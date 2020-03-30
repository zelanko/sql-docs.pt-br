---
title: Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1610f98d77ba4a762a63f3ccf5a445393537d36b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296335"
---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 No Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode definir o nome, o tipo de dados e as propriedades do tipo de dados das colunas nas novas tabelas e arquivos de destino, mas não é possível especificar conversões personalizadas para valores de coluna. Como resultado, o mapeamento interno dos tipos de dados de origem para destino é importante.  
  
##  <a name="how-does-the-wizard-map-data-types-between-source-and-destination"></a><a name="wizardMapping"></a> Como o assistente mapeia tipos de dados entre a origem e o destino?
O assistente usa arquivos de mapeamento que são instalados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para mapear os tipos de dados de um sistema ou versão de um banco de dados para outro. Por exemplo, é possível mapear do tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tipos de dados Oracle. Por padrão, os arquivos de mapeamento em formato XML são instalados nas seguintes pastas.
-   **C:\Arquivos de Programas\Microsoft SQL Server\130\DTSMappingFiles\\** (para 64 bits)
-   **C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\DTSMappingFiles\\** (para 32 bits).  
  
 Se editar um arquivo de mapeamento existente ou adicionar um novo arquivo de mapeamento à pasta, você deverá fechar e reabrir o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para carregar os arquivos novos ou alterados.  
 
## <a name="you-can-change-an-existing-mapping-file"></a>Você pode alterar um arquivo de mapeamento existente
Se sua empresa exigir mapeamentos diferentes entre tipos de dados, você poderá atualizar os arquivos de mapeamentos para alterar os mapeamentos usados pelo assistente. Por exemplo, se você quiser que o tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** do seja mapeado para o tipo de dados **GRAPHIC** do DB2 em vez do tipo dados **VARGRAPHIC** do DB2, ao transferir dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o DB2, altere o mapeamento de **nchar** no arquivo de mapeamento **SqlClientToIBMDB2.xml** para usar **GRAPHIC** em vez de **VARGRAPHIC.**  
  
## <a name="you-can-add-a-new-mapping-file"></a>Você pode adicionar um novo arquivo de mapeamento
O[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala mapeamentos entre muitas combinações de origem e de destino usadas com frequência. Você também pode adicionar novos arquivos de mapeamento para o diretório **MappingFiles** para dar suporte a outras origens e destinos. Os novos arquivos de mapeamento devem estar em conformidade com o esquema XSD publicado e devem mapear uma combinação exclusiva de origem e destino. O esquema para arquivos de mapeamento, **DataTypeMapping.xsd**, é publicado [aqui](https://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd).
 
## <a name="sample-mapping-file"></a>Exemplo de arquivo de mapeamento
Esta é uma parte do arquivo de mapeamento XML que mapeia de tipos de dados do SQL Server (ou, mais especificamente, dos tipos de dados usados pelo Provedor de Dados .Net Framework para SQL Server) para tipos de dados Oracle. Como um exemplo, você pode ver que um tipo de dados **int** do SQL Server é mapeado para um tipo de dados **INTEGER** do Oracle.
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="https://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  

