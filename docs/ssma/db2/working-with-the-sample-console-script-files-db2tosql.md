---
title: Trabalhando com os arquivos de Script de Console de exemplo (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5c3080c3-d074-4f99-a5f5-219ebeddc474
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dc7976fae322dddc24eda7cf6ef84ef20a7a9e61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259009"
---
# <a name="working-with-the-sample-console-script-files-db2tosql"></a>Trabalhando com os arquivos de Script de Console de exemplo (DB2ToSQL)
Alguns arquivos de exemplo foram fornecidos juntamente com o produto para a referência de usuário e o uso. Esta seção descreve a maneira de personalizar facilmente esses scripts para as necessidades do usuário final.  
  
## <a name="sample-console-script-files"></a>Arquivos de Script de Console de exemplo  
Os seguintes arquivos de script de console de exemplo que abrangem cenários diferentes foram fornecidos para referência de usuário:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
1.  **ServersConnectionFileSample.xml:**  
  
    -   Este exemplo fornece os diferentes modos de conexão disponível para o banco de dados de origem e de destino e o usuário pode selecionar qualquer modo, de acordo com o requisito. Este exemplo contém as definições de servidor.  
  
    -   O usuário pode se conectar ao banco de dados necessário, simplesmente alterando os valores para a origem necessários e definições de servidor de destino. No exemplo fornecido todos os valores foram fornecidos valores como variáveis que estão disponíveis na **VariableValueFileSample.xml**.  Todos os outros parâmetros de conexão podem ser removidos do arquivo de conexão de servidor de trabalho do usuário.  
  
    -   Para obter mais informações sobre como se conectar ao servidor de origem e destino, consulte [criar os arquivos de Conexão de servidor &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-the-server-connection-files-db2tosql.md) .  
  
2.  **VariableValueFileSample.xml:** Arquivos de script de todas as variáveis que foram usadas no console do exemplo e `ServersConnectionFileSample.xml` foram agrupadas nesse arquivo. Para executar os scripts de console de exemplo que o usuário tem que simplesmente substituir a variável de exemplo valores com o usuário definido aqueles e passam esse arquivo como um argumento de linha de comando adicionais, juntamente com o arquivo de script.  
  
    Para obter mais informações sobre o arquivo de valor de variável, consulte [criando arquivos de valor de variável &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md).  
  
3.  **AssessmentReportGenerationSample.xml:** Este exemplo permite ao usuário gerar um relatório de avaliação de xml que pode ser usado pelo usuário para análise antes que ele comece a converter e migrar os dados.  
  
    No `generate-assessment-report` o usuário deve alterar mandatorily o valor da variável de comando (consulte **VariableValueFileSample.xml**) na `object-name` do atributo a ser o nome de banco de dados em uso pelo usuário. Dependendo do tipo de objeto especificado, o `object-type` valor também terá que ser alterado.  
  
    Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `generate-assessment-report` 4 de exemplo do comando do exemplo de arquivo de script de console.  
  
    Para obter mais informações sobre como gerar relatórios, consulte [geração de relatórios &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
    **Observações:**  
  
    Certifique-se de que o argumento de linha de comando do arquivo de valor da variável é passado para o aplicativo de console e VariableValueFileSample.xml é atualizado com o usuário especificado valores.  
  
    Certifique-se de que o argumento de linha de comando de arquivo de conexão de servidor é passado para o aplicativo de console e o ServersConnectionFileSample.xml é atualizado com os valores de parâmetro de servidor correto.  
  
4.  **SqlStatementConversionSample.xml:** Este exemplo permite que o usuário gere correspondente `t-sql` script para o banco de dados de origem `sql` comando fornecido como entrada.  
  
    No `convert-sql-statement` o usuário deve alterar mandatorily o valor da variável de comando (consulte **VariableValueFileSample.xml**) na `context` do atributo como o nome do banco de dados que está sendo utilizado pelo usuário. O usuário também precisará alterar o `sql` valor de atributo para o banco de dados de origem `sql` comando que ele exija a ser convertido.  
  
    O usuário também pode fornecer arquivos sql a ser convertido. Isso tem sido ilustrado no `convert-sql-statement` 4 de exemplo do comando do exemplo de arquivo de script de console.  
  
    > [!NOTE]  
    > Certifique-se de que o argumento de linha de comando do arquivo de valor da variável é passado para o aplicativo de console e VariableValueFileSample.xml é atualizado com o usuário especificado valores.  
  
5.  **ConversionAndDataMigrationSample.xml:** Este exemplo permite que o usuário executar uma migração de ponta a ponta da conversão para a migração de dados. A lista de valores de atributo obrigatório que eles terão de alterar é listada abaixo:  
  
    |Nome do comando|Descrição|attribute|  
    |----------------|---------------|-------------|  
    |`map-schema`|Mapeamento de esquema de banco de dados de origem ao esquema de destino.|`source-schema:` Especifica o banco de dados de origem que requer a ser convertido.<br /><br />`sql-server-schema`: Especifica o banco de dados de destino que deve ser migrados para o|  
    |`convert-schema`|Executa a conversão de esquema de origem ao esquema de destino.<br /><br />Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `convert-schema` 4 de exemplo do comando do exemplo de arquivo de script de console.|`object-name`: Especifique o banco de dados de origem / nome que exige a ser convertido do objeto. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`|  
    |`synchronize-target`|Sincroniza os objetos de destino com o banco de dados de destino.<br /><br />Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `synchronize-target` 3 de exemplo do comando do exemplo de arquivo de script de console.|`object-name:` Especifique o banco de dados do sql server / nome que exige a criação do objeto. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`|  
    |`migrate-data`|Migra os dados de origem para o destino.<br /><br />Se o usuário tem que avaliar vários objetos / bancos de dados ele pode especificar vários `metabase-object` nós conforme ilustrado no `migrate-data` 2 do exemplo do comando do exemplo de arquivo de script de console.|`object-name:` Especifica o banco de dados de origem / tabelas nome que exige a serem migrados. Certifique-se de que o correspondente `object-type` é alterada com base no tipo de objeto que é especificado no `object-name`|  
  
## <a name="see-also"></a>Consulte também  
[Criando arquivos de valor da variável &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
[Criar os arquivos de Conexão de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
[Geração de relatórios &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)  
  
