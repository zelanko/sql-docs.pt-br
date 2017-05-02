---
title: "Configurar Espaços de Armazenamento com um cache de write-back de NVDIMM-N | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a0a115eba3fbd1afe52c211fe0f93362a989fc2
ms.lasthandoff: 04/11/2017

---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>Configurar Espaços de Armazenamento com um cache de write-back de NVDIMM-N
  O Windows Server 2016 dá suporte a dispositivos NVDIMM-N que permitem operações de E/S (entrada/saída) extremamente rápidas. Uma maneira interessante de usar dispositivos como esses é como um cache com write-back para obter latências de gravação baixas. Este tópico aborda como configurar um espaço de armazenamento espelhado com um cache de write-back de NVDIMM-N espelhado como uma unidade virtual para armazenar o log de transações do SQL Server. Se você pretende utilizá-lo para armazenar também outros dados ou tabelas de dados, é possível incluir mais discos no pool de armazenamento, ou criar vários pools, caso o isolamento seja importante.  
  
 Para exibir um vídeo do Channel 9 que usa essa técnica, veja [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016](https://channel9.msdn.com/Events/Build/2016/P466)(Usando a memória não volátil (NVDIMM-N) como bloco de armazenamento no Windows Server 2016).  
  
## <a name="identifying-the-right-disks"></a>Identificando os discos certos  
 A configuração dos espaços de armazenamento no Windows Server 2016, especialmente com recursos avançados, como caches de write-back, é feita com mais facilidade por meio do PowerShell. A primeira etapa é identificar quais discos devem fazer parte do pool de Espaços de Armazenamento com base nos quais o disco virtual será criado. NVDIMM-Ns tem um tipo de mídia e tipo de barramento de SCM (memória de classe de armazenamento) que pode ser consultado por meio do cmdlet Get-PhysicalDisk do PowerShell.  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  Com dispositivos NVDIMM-N, você não precisa mais selecionar especificamente os dispositivos que podem ser destinos do cache de write-back.  
  
 Para criar um disco virtual espelhado com cache de write-back espelhado, são necessários, pelo menos, dois NVDIMM-Ns e dois outros discos. Atribuir os discos físicos desejados a uma variável antes da criação do pool facilita o processo.  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 A captura de tela mostra a variável $pd, bem como os dois SSDs e dois NVDIMM-Ns aos quais ela foi atribuída, retornada usando o cmdlet do PowerShell a seguir.  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Select FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## <a name="creating-the-storage-pool"></a>Criando o pool de armazenamento  
 Com a variável $pd que contém PhysicalDisks, é fácil criar o pool de armazenamento usando o cmdlet New-StoragePool do PowerShell.  
  
```  
New-StoragePool –StorageSubSystemFriendlyName “Windows Storage*” –FriendlyName NVDIMM_Pool –PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>Criando o disco virtual e o volume  
 Agora que um pool foi criado, a próxima etapa é criar um disco virtual e formatá-lo. Nesse caso, apenas um disco virtual será criado e o cmdlet New-Volume do PowerShell poderá ser usado para simplificar esse processo:  
  
```  
New-Volume –StoragePool (Get-StoragePool –FriendlyName NVDIMM_Pool) –FriendlyName Log_Space –Size 300GB –FileSystem NTFS –AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 O disco virtual foi criado, inicializado e formatado com NTFS. A captura de tela abaixo mostra que ele tem um tamanho de 300 GB e um tamanho de cache de gravação de 1 GB, que será hospedado nos NVDIMM-Ns.  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 Agora você pode exibir esse novo volume visível em seu servidor. Agora você pode usar essa unidade para o log de transações do SQL Server.  
  
 ![Log_Space Drive](../../relational-databases/performance/media/log-space-drive.png "Log_Space Drive")  
  
## <a name="see-also"></a>Consulte também  
 [Espaços de Armazenamento do Windows no Windows 10](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)   
 [Espaços de Armazenamento do Windows no Windows 2012 R2](https://technet.microsoft.com/en-us/library/hh831739.aspx)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Exibir ou alterar os locais padrão de arquivos de log e de dados &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  
