---
title: Local de armazenamento de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f3fa3c8520d4927297ec56898a181502b0664de0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="database-storage-location"></a>Local de armazenamento do banco de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Geralmente há situações quando um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] administrador de banco de dados (dba) quer um determinado banco de dados resida fora da pasta de dados do servidor. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como melhorar o desempenho ou expandir o armazenamento. Para tais situações, a propriedade **DbStorageLocation** do banco de dados permite que o dba [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especifique o local do banco de dados em um disco local ou dispositivo de rede.  
  
## <a name="dbstoragelocation-database-property"></a>Propriedade DbStorageLocation do banco de dados  
 A propriedade **DbStorageLocation** do banco de dados especifica a pasta na qual o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria e gerencia todos os dados de banco de dados e arquivos de metadados. Todos os arquivos de metadados são armazenados na pasta **DbStorageLocation** , com exceção do arquivo de metadados do banco de dados, pois ele é armazenado na pasta de dados do servidor. Existem duas considerações importantes ao definir o valor da propriedade **DbStorageLocation** do banco de dados:  
  
-   A propriedade **DbStorageLocation** do banco de dados deve ser definida como um caminho de pasta UNC existente ou uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia é o padrão para a pasta de dados do servidor. Se a pasta não existir, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
-   A propriedade **DbStorageLocation** do banco de dados não pode ser definida para apontar para a pasta de dados do servidor nem para uma de suas subpastas. Se o local apontar para a pasta de dados do servidor ou qualquer uma de suas subpastas, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
> [!IMPORTANT]  
>  É recomendável definir o caminho UNC para usar uma SAN (Rede de Área de Armazenamento), uma rede baseada em iSCSI ou um disco anexado localmente. Qualquer caminho UNC para um compartilhamento de rede ou qualquer solução de armazenamento remoto de alta latência leva a uma instalação sem suporte.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>Comparação entre DbStorageLocation e StorageLocation  
 **DbStorageLocation** especifica a pasta em que estão todos os arquivos de metadados e dados do banco de dados, enquanto **StorageLocation** especifica a pasta em que está uma ou mais partições de um cubo. **StorageLocation** pode ser definido de forma independente de **DbStorageLocation**. Esta é uma decisão do dba do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com base nos resultados esperados e muitas vezes sobreporá o uso de uma propriedade ou outra.  
  
## <a name="dbstoragelocation-usage"></a>O uso de DbStorageLocation  
 A propriedade **DbStorageLocation** é usada como parte de um comando **Create** em uma sequência de comandos **Detach**/**Attach** do banco de dados, em uma sequência de comandos **Backup**/**Restore** do banco de dados ou em um comando **Synchronize** do banco de dados. Ao alterar a propriedade **DbStorageLocation** do banco de dados, consideramos uma alteração estrutural no objeto de banco de dados. Isso significa que todos os metadados devem ser recriados e os dados devem ser reprocessados.  
  
> [!IMPORTANT]  
>  Você não deve alterar o local de armazenamento do banco de dados usando um comando **Alter** . Em vez disso, recomendamos usar uma sequência dos comandos de banco de dados **Detach**/**Attach** (consulte [Mover um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md), [Anexar e desanexar Bancos de Dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um banco de dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Elemento DbStorageLocation](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)   
 [Criar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Sincronizar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)  
  
  
