---
title: Selecionar e configurar os objetos afetados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: fbd151b0fa8682865e44615c22a9fdd7577014ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62626520"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>Selecionar e configurar os objetos afetados (OracleToSQL)
Nessa página, você pode selecionar tabelas e chaves estrangeiras, as alterações no qual devem ser comparadas ao SSMA verifica os resultados da execução para os objetos escolhidos na etapa anterior. Além disso, você pode personalizar os parâmetros de verificação.  
  
## <a name="selection-of-affected-objects"></a>Seleção de objetos afetados  
Na árvore de objetos de Oracle localizado no lado esquerdo da janela, verifique as tabelas e chaves estrangeiras, as alterações na qual devem ser comparadas para serem idênticos.  
  
Se o testador SSMA não é possível verificar qualquer um desses objetos, você verá o link rotulado **alguns objetos selecionados contêm erros** abaixo da árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser comparados e desmarque a seleção de objetos errados.  
  
## <a name="table"></a>Table  
Na guia da tabela contém a exibição de grade da tabela selecionada. A grade contém as seguintes informações sobre a tabela selecionada:  
  
-   Nome da coluna  
  
-   Tipo de Dados  
  
-   Precisão  
  
-   Escala  
  
-   Regra  
  
-   Padrão  
  
-   Identidade  
  
-   Anulável  
  
## <a name="sql"></a>Sql  
Guia SQL contém a tabela"criar" SQL da tabela selecionada.  
  
## <a name="data"></a>Dados  
Guia de dados exibe dados presentes na tabela selecionada.  
  
## <a name="properties"></a>Propriedades  
Guia de propriedades exibe as propriedades da tabela selecionada. Os campos a seguir estão presentes na guia Propriedades:  
  
-   Criado ou modificado pela última vez  
  
-   Object Name  
  
## <a name="columns-comparison-settings"></a>Configurações de comparação de colunas  
Estabelecer as regras de comparação para colunas de tabela no **comparação de colunas** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Use durante as comparações de teste  
Determine se essa coluna farão parte de verificação de resultados de teste.  
  
-   Se você escolher **verdadeira**, SSMA irá comparar o conteúdo desta coluna depois de executar o teste no Oracle com o conteúdo da coluna no SQL Server. 
  
-   Se você escolher**falsos**, a coluna será excluída da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para colunas de tipo de dados numérico, você pode definir um dimensionamento personalizado para a comparação.  
  
-   Se você escolher **verdadeira**, valores numéricos serão arredondados de acordo com o **comparando escala** valor antes de serem comparadas.  
  
-   Se você escolher**falsos**, a comparação numérica será ser exata.  
  
### <a name="comparing-scale"></a>Comparação de escala  
  
-   Disponível somente se o **escala personalizada de uso** opção for definida como **verdadeiro**. Isso é a precisão de comparação numérica.  
  
### <a name="date-time-comparing"></a>Comparação de tempo de data  
Define como a data/hora valores são comparados.  
  
-   Se você selecionar **comparar todo data**, será executada uma comparação completa de valores de ambas as plataformas.  
  
-   Se você selecionar **comparar apenas data**, a hora em que parte será ignorada.  
  
-   Se você selecionar **comparar apenas hora**, a data em que parte será ignorada.  
  
-   Se você selecionar **milissegundos ignorar**, os resultados serão comparados até segundos.  
  
-   Se você selecionar **data ignorar e milissegundos**, o resultado será em comparação com apenas por parte do tempo e ignorando partes fracionárias de um segundo.  
  
### <a name="ignore-strings-case"></a>Ignorar maiusculas e minúsculas de cadeias de caracteres  
Controla a diferenciação de maiusculas da comparação.  
  
-   Se você escolher **verdadeira**, a comparação será diferencia maiusculas de minúsculas.  
  
-   Se você escolher **falsos**, a comparação considerará diferenciar maiusculas e minúsculas.  
  
## <a name="comparing-sql"></a>Comparando o SQL  
Você pode exibir as instruções SELECT geradas pelo testador do SSMA na **comparando SQL** página. O testador comparará os conjuntos de resultados dessas instruções em uma base linha por linha. Cada linha seguinte de um conjunto de resultados do Oracle deve ser igual para a próxima linha do conjunto de resultados produzido no SQL Server.
  
Você pode editar essas instruções SELECT para fornecer verificação personalizada. Para salvar as alterações no Oracle e nas instruções do SQL Server, use o **aplicar** botões na origem e de destino SQL, de forma correspondente.  
  
## <a name="next-step"></a>Próxima etapa  
[Personalizando a ordem das chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Concluir a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[Executar casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
