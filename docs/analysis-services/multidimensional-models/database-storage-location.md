---
title: Local de armazenamento do banco de dados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0544e7e7d552098806d4c3d93751631d03520139
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62714793"
---
# <a name="database-storage-location"></a>Local de armazenamento do banco de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Existem situações frequentes em que um administrador de banco de dados (dba) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deseja que determinados bancos de dados estejam fora da pasta de dados do servidor. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como melhorar o desempenho ou expandir o armazenamento. Para tais situações, a propriedade **DbStorageLocation** do banco de dados permite que o dba [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especifique o local do banco de dados em um disco local ou dispositivo de rede.  
  
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
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar Bancos de Dados do Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover um Banco de Dados do Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)  
  
  
