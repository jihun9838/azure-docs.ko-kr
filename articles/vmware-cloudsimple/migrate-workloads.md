---
title: Azure VMware 솔루션 (AVS)-작업 Vm을 AVS 사설 클라우드로 마이그레이션
description: 온-프레미스 vCenter에서 AVS 사설 클라우드 vCenter로 가상 컴퓨터를 마이그레이션하는 방법에 대해 설명 합니다.
author: sharaths-cs
ms.author: b-shsury
ms.date: 08/20/2019
ms.topic: article
ms.service: azure-vmware-cloudsimple
ms.reviewer: cynthn
manager: dikamath
ms.openlocfilehash: af02bd947c73b670306704a10a09ca981b34c9a9
ms.sourcegitcommit: 21e33a0f3fda25c91e7670666c601ae3d422fb9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2020
ms.locfileid: "77019998"
---
# <a name="migrate-workload-vms-from-on-premises-vcenter-to-avs-private-cloud-vcenter-environment"></a>온-프레미스 vCenter에서 AVS 사설 클라우드 vCenter 환경으로 워크 로드 Vm 마이그레이션

온-프레미스 데이터 센터에서 AVS 사설 클라우드로 Vm을 마이그레이션하려면 몇 가지 옵션을 사용할 수 있습니다. AVS 사설 클라우드는 VMware vCenter에 대 한 기본 액세스를 제공 하며 VMware에서 지원 되는 도구는 워크 로드 마이그레이션에 사용할 수 있습니다. 이 문서에서는 몇 가지 vCenter 마이그레이션 옵션을 설명 합니다.

## <a name="prerequisites"></a>필수 조건

온-프레미스 데이터 센터에서 Vm 및 데이터를 마이그레이션하려면 데이터 센터에서 AVS 사설 클라우드 환경으로 네트워크를 연결 해야 합니다. 다음 방법 중 하나를 사용 하 여 네트워크 연결을 설정 합니다.

* 온-프레미스 환경과 AVS 사설 클라우드 간의 [사이트 간 VPN 연결](vpn-gateway.md#set-up-a-site-to-site-vpn-gateway) .
* Express 경로 Global Reach 온-프레미스 Express 경로 회로와 AVS Express 경로 회로 간의 연결입니다.

온-프레미스 vCenter 환경에서 AVS 사설 클라우드로의 네트워크 경로는 vMotion을 사용 하 여 Vm을 마이그레이션하는 데 사용할 수 있어야 합니다. 온-프레미스 vCenter의 vMotion 네트워크에는 라우팅 기능이 있어야 합니다. 방화벽이 온-프레미스 vCenter와 AVS 사설 클라우드 vCenter 간의 모든 vMotion 트래픽을 허용 하는지 확인 합니다. (AVS 사설 클라우드에서 vMotion 네트워크의 라우팅은 기본적으로 구성 됩니다.)

## <a name="migrate-isos-and-templates"></a>Iso 및 템플릿 마이그레이션

AVS 사설 클라우드에서 새 가상 컴퓨터를 만들려면 Iso 및 VM 템플릿을 사용 합니다. Iso 및 템플릿을 AVS 사설 클라우드 vCenter에 업로드 하 고 사용할 수 있게 하려면 다음 방법을 사용 합니다.

1. VCenter UI에서 AVS 사설 클라우드 vCenter에 ISO를 업로드 합니다.
2. AVS 사설 클라우드 vCenter에 [콘텐츠 라이브러리를 게시](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vm_admin.doc/GUID-2A0F1C13-7336-45CE-B211-610D39A6E1F4.html) 합니다.

    1. 온-프레미스 콘텐츠 라이브러리를 게시 합니다.
    2. AVS 사설 클라우드 vCenter에서 새 콘텐츠 라이브러리를 만듭니다.
    3. 게시 된 온-프레미스 콘텐츠 라이브러리를 구독 합니다.
    4. 구독 한 콘텐츠에 대 한 액세스를 위해 콘텐츠 라이브러리를 동기화 합니다.

## <a name="migrate-vms-using-powercli"></a>PowerCLI를 사용 하 여 Vm 마이그레이션

온-프레미스 vCenter에서 AVS 사설 클라우드 vCenter로 Vm을 마이그레이션하려면 vmware Labs에서 사용할 수 있는 VMware PowerCLI 또는 크로스 vCenter 워크 로드 마이그레이션 유틸리티를 사용 합니다. 다음 샘플 스크립트는 PowerCLI 마이그레이션 명령을 보여 줍니다.

```
$sourceVC = Connect-VIServer -Server <source-vCenter name> -User <source-vCenter user name> -Password <source-vCenter user password>
$targetVC = Connect-VIServer -Server <target-vCenter name> -User <target-vCenter user name> -Password <target-vCenter user password>
$vmhost = <name of ESXi host on destination>
$vm = Get-VM -Server $sourceVC <name of VM>
Move-VM -VM $vm -VMotionPriority High -Destination (Get-VMhost -Server $targetVC -Name $vmhost) -Datastore (Get-Datastore -Server $targetVC -Name <name of tgt vc datastore>)
```

> [!NOTE]
> 대상 vCenter 서버 및 ESXi 호스트의 이름을 사용 하려면 온-프레미스에서 AVS 사설 클라우드로의 DNS 전달을 구성 합니다.

## <a name="migrate-vms-using-nsx-layer-2-vpn"></a>NSX Layer 2 VPN을 사용 하 여 Vm 마이그레이션

이 옵션을 사용 하면 온-프레미스 VMware 환경에서 Azure의 AVS 사설 클라우드로 작업을 실시간으로 마이그레이션할 수 있습니다. 이 스트레치 된 계층 2 네트워크를 사용 하 여 온-프레미스의 서브넷은 AVS 사설 클라우드에서 사용할 수 있습니다. 마이그레이션 후 Vm에 대 한 새 IP 주소 할당은 필요 하지 않습니다.

[계층 2 스트레치 네트워크를 사용 하 여 워크 로드 마이그레이션](migration-layer-2-vpn.md) 계층 2 VPN을 사용 하 여 온-프레미스 환경에서 계층 2 네트워크를 AVS 사설 클라우드로 스트레치 하는 방법을 설명 합니다.

## <a name="migrate-vms-using-backup-and-disaster-recovery-tools"></a>백업 및 재해 복구 도구를 사용 하 여 Vm 마이그레이션

백업/복원 도구 및 재해 복구 도구를 사용 하 여 Vm을 AVS 사설 클라우드로 마이그레이션할 수 있습니다. 타사 도구를 사용 하 여 만든 백업에서 복원 하려면 AVS 사설 클라우드를 대상으로 사용 합니다. 또한 AVS 사설 클라우드는 VMware SRM 또는 타사 도구를 사용 하 여 재해 복구를 위한 대상으로 사용할 수 있습니다.

이러한 도구를 사용 하는 방법에 대 한 자세한 내용은 다음 항목을 참조 하세요.

* [Veeam B & R을 사용 하 여 AVS 사설 클라우드의 워크 로드 가상 머신 백업](backup-workloads-veeam.md)
* [온-프레미스 VMware 워크 로드에 대 한 재해 복구 사이트로 AVS 사설 클라우드 설정](disaster-recovery-zerto.md)
