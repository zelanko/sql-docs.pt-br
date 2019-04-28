---
title: Local de armazenamento do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c4f46a78941b527b809fd17d7d82946cce1b8af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62700097"
---
# <a name="database-storage-location"></a>Local de armazenamento do banco de dados
  Existem situações frequentes em que um administrador de banco de dados (dba) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deseja que determinados bancos de dados estejam fora da pasta de dados do servidor. Essas situações frequentemente são conduzidas pelas necessidades comerciais, como melhorar o desempenho ou expandir o armazenamento. Nessas situações, o `DbStorageLocation` permite que a propriedade de banco de dados a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba para especificar o local do banco de dados em um dispositivo de disco ou rede local.  
  
## <a name="dbstoragelocation-database-property"></a>Propriedade DbStorageLocation do banco de dados  
 A propriedade `DbStorageLocation` do banco de dados especifica a pasta onde o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria e gerencia todos os dados de banco de dados e arquivos de metadados. Todos os arquivos de metadados são armazenados na pasta `DbStorageLocation`, com exceção do arquivo de metadados do banco de dados, pois ele é armazenado na pasta de dados do servidor. Existem duas considerações importantes ao definir o valor da propriedade `DbStorageLocation` do banco de dados:  
  
-   A propriedade `DbStorageLocation` do banco de dados deve ser definida como um caminho de pasta UNC existente ou uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia é o padrão para a pasta de dados do servidor. Caso a pasta não exista, ocorrerá um erro quando você executar um comando `Create`, `Attach` ou `Alter`.  
  
-   A propriedade `DbStorageLocation` do banco de dados não pode ser definida para apontar a pasta de dados do servidor ou qualquer uma de suas subpastas. Se o local aponta para para a pasta de dados do servidor ou qualquer uma de suas subpastas, ocorrerá um erro quando você executar um comando `Create`, `Attach` ou `Alter`.  
  
> [!IMPORTANT]  
>  É recomendável definir o caminho UNC para usar uma SAN (Rede de Área de Armazenamento), uma rede baseada em iSCSI ou um disco anexado localmente. Qualquer caminho UNC para um compartilhamento de rede ou qualquer solução de armazenamento remoto de alta latência leva a uma instalação sem suporte.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>Comparação entre DbStorageLocation e StorageLocation  
 `DbStorageLocation` especifica a pasta em que estão todos os arquivos de metadados e dados do banco de dados, enquanto que `StorageLocation` especifica a pasta em que está uma ou mais partições de um cubo. `StorageLocation` pode ser definida de maneira independente de `DbStorageLocation`. Esta é uma decisão do dba do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com base nos resultados esperados e muitas vezes sobreporá o uso de uma propriedade ou outra.  
  
## <a name="dbstoragelocation-usage"></a>O uso de DbStorageLocation  
 O `DbStorageLocation` propriedade de banco de dados é usada como parte de uma `Create` comando no banco de dados um `Detach` / `Attach` comandos de banco de dados de sequência, em um `Backup` / `Restore` sequência de comandos de banco de dados , ou em um `Synchronize` comando de banco de dados. Ao alterar a propriedade `DbStorageLocation` do banco de dados, consideramos uma alteração estrutural no objeto de banco de dados. Isso significa que todos os metadados devem ser recriados e os dados devem ser reprocessados.  
  
> [!IMPORTANT]  
>  Você não deve alterar o local de armazenamento do banco de dados usando um comando `Alter`. Em vez disso, é recomendável que você use uma sequência de `Detach` / `Attach` comandos de banco de dados (consulte [mover um banco de dados do Analysis Services](move-an-analysis-services-database.md), [anexar e desanexar o Analysis Services Databases](attach-and-detach-analysis-services-databases.md)).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar Bancos de Dados do Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Mover um Banco de Dados do Analysis Services](move-an-analysis-services-database.md)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)   
 [Elemento Create &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)  
  
  
