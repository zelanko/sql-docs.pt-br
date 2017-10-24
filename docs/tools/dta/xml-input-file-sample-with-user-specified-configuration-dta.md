---
title: "Exemplo de arquivo com a configuração especificada pelo usuário (DTA) de entrada XML | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b11febc0d8f432453516237b93a753a588014691
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)
  Copie e cole este exemplo de um arquivo de entrada XML que especifica uma configuração especificada pelo usuário com o elemento **Configuration** em seu editor XML ou editor de texto favorito. Isso permite realizar uma análise hipotética. A análise hipotética envolve o uso do elemento **Configuration** para especificar um conjunto de estruturas de design físico hipotéticas para o banco de dados que você deseja ajustar. Então você usa o Orientador de Otimização do Mecanismo de Banco de Dados para analisar os efeitos de executar uma carga de trabalho em relação a essa configuração hipotética para descobrir se ela melhorará o desempenho de processamento de consulta. Esse tipo de análise oferece a vantagem de poder avaliar a nova configuração sem incorrer na sobrecarga da implementação de fato. Se sua configuração hipotética não oferecer a melhora de desempenho desejada, é fácil alterá-la e fazer novas análises até que você alcance a configuração que produza os resultados necessários.  
  
 Depois de copiar esse exemplo em sua ferramenta de edição, substitua os valores especificados para os elementos **Servidor**, **Banco de Dados**, **Esquema**, **Tabela**, **Carga de trabalho**, **Opções de Ajuste**e **Configuração** com aqueles para sua sessão de ajuste específica. Para obter mais informações sobre todos os atributos e elementos filho que podem ser usados com esses elementos, veja a [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md). O exemplo a segui usa um subconjunto de atributo único disponível e opções de elemento filho.  
  
## <a name="code"></a>Código  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
<!-- To tune multiple databases, list them and their associated tables in the following section. -->  
      <Database>  
        <Name>MyDatabaseName</Name>  
        <Schema>  
          <Name>MyDatabaseSchemaName</Name>  
<!-- You can list as many tables as necessary in the following section. -->  
          <Table>  
            <Name>MyTableName1</Name>  
          </Table>  
          <Table>  
            <Name>MyTableName2</Name>  
          </Table>  
        </Schema>  
      </Database>  
    </Server>  
    <Workload>  
<!-- The following element specifies a workload file, which can be a trace file or a Transact-SQL script file. -->  
      <File>c:\PathToYourWorkloadFile</File>  
    </Workload>  
    <TuningOptions>  
      <TuningTimeInMin>180</TuningTimeInMin>  
      <StorageBoundInMB>10000</StorageBoundInMB>  
      <FeatureSet>IDX_IV</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
      <OnlineIndexOperation>OFF</OnlineIndexOperation>  
    </TuningOptions>  
    <Configuration SpecificationMode="Absolute">  
      <Server>  
        <Name>MyServerName</Name>  
          <Database>  
            <Name>MyDatabaseName</Name>  
            <Schema>  
              <Name>MyDatabaseSchemaName</Name>  
                <Table>  
                  <Name>MyTableName1</Name>  
                  <Recommendation>  
                    <Create>  
                      <Index Clustered="true" Unique="false" Online="false" IndexSizeInMB="873.75">  
                        <Name>MyIndexName</Name>  
                        <Column Type="KeyColumn" SortOrder="Ascending">  
                          <Name>MyColumnName1</Name>  
                        </Column>  
                        <Filegroup>MyFileGroupName1</FileGroup>  
                      </Index>  
                    </Create>  
                  </Recommendation>  
                </Table>  
            </Schema>  
          </Database>  
      </Server>  
    </Configuration>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="comments"></a>Comentários  
  
-   A remoção das estruturas de design físico não terá suporte caso você especifique o modo **Absoluto** para o elemento **Configuration** (`Configuration SpecificationMode="Absolute"`).  
  
-   Não é possível criar e remover a mesma estrutura de design físico em qualquer um dos modos (**Relative** ou **Absolute**) do elemento **Configuration** .  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Exibir e trabalhar com a saída do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

