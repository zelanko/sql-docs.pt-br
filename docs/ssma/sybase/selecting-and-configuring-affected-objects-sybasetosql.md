---
title: Selecionando e configurando aos objetos afetados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9871370dc3e6e8ca9d148a4df2435ce94286903
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>Selecionando e configurando aos objetos afetados (SybaseToSQL)
Nesta página, você pode selecionar tabelas e chaves estrangeiras, alterações em que devem ser comparadas ao SSMA verifica os resultados da execução para os objetos escolhidos na etapa anterior. Além disso, você pode personalizar os parâmetros de verificação.  
  
## <a name="selection-of-affected-objects"></a>Seleção de objetos afetados  
Na árvore de objetos do Sybase localizado no lado esquerdo da janela, marque as tabelas e chaves estrangeiras, alterações em que devem ser comparadas para sejam idênticos.  
  
Se o SSMA Tester não é possível verificar qualquer um desses objetos, você verá o link rotulado **alguns objetos selecionados contêm erros** na árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser comparados e desmarque a seleção de objetos errados.  
  
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
Guia do SQL contém a tabela"criar" SQL da tabela selecionada.  
  
## <a name="data"></a>data  
Guia de dados exibe dados presentes na tabela selecionada.  
  
## <a name="properties"></a>Propriedades  
Guia de propriedades exibe as propriedades da tabela selecionada. Os campos a seguir estão presentes na guia Propriedades:  
  
-   Criado ou modificado pela última vez  
  
-   Object Name  
  
## <a name="table-comparison-settings"></a>Configurações de tabela de comparação  
Estabelecer as regras de comparação para a tabela na **comparações de tabelas** página. Você pode fazer as seguintes configurações.  
  
### <a name="comparison-mode"></a>Modo de comparação  
Define o conteúdo da tabela na qual será realizada a comparação.  
  
-   Se você selecionar **apenas alterações**, comparação de linhas de tabela será executada.  
  
-   Se você selecionar **completo**, a comparação somente as linhas que foram alteradas será executada.  
  
## <a name="column-comparison-settings"></a>Configurações de comparação de coluna  
Estabelecer as regras de comparação para colunas de tabela em **coluna comparações** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Use durante as comparações de teste  
Determine se essa coluna participará na verificação de resultados de teste.  
  
-   Se você escolher **True**, SSMA irá comparar o conteúdo dessa coluna depois da execução de teste em Sybase com o conteúdo da coluna no SQL Server.
  
-   Se você escolher **False**, a coluna será excluída da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para colunas de tipo de dados numérico, você pode definir uma escala personalizada para a comparação.  
  
-   Se você escolher **True**, valores numéricos serão arredondados de acordo com o **comparando escala** valor antes de serem comparadas.  
  
-   Se você escolher **False**, a comparação numérica será exata.  
  
### <a name="comparing-scale"></a>Comparação de escala  
  
-   Disponível somente se o **escala personalizada de uso** opção é definida como **True**. Isso é a precisão para comparação numérica.  
  
### <a name="date-time-comparing"></a>Comparação de tempo de data  
Define como a data/hora valores são comparados.  
  
-   Se você selecionar **comparar todo data**, comparação de valores de ambas as plataformas será executada.  
  
-   Se você selecionar **comparar apenas data**, o tempo de parte será ignorada.  
  
-   Se você selecionar **comparar apenas tempo**, a data de parte será ignorada.  
  
-   Se você selecionar **milissegundos ignorar**, os resultados serão comparados em segundos.  
  
-   Se você selecionar **data ignorar e milissegundos**, o resultado será comparados apenas por parte do tempo e ignorando partes frações de segundo.  
  
### <a name="ignore-strings-case"></a>Ignorar maiusculas e minúsculas cadeias de caracteres  
Controla a diferenciação de maiusculas e minúsculas da comparação.  
  
-   Se você escolher **True**, a comparação diferenciará maiusculas e minúsculas.  
  
-   Se você escolher **False**, a comparação será conta para diferenciar maiusculas de minúsculas.  
  
## <a name="comparing-sql"></a>Comparando SQL  
Você pode exibir as instruções SELECT geradas pelo testador SSMA no **SQL comparar** página. O testador comparará os conjuntos de resultados das instruções a seguir em uma base linha por linha. Cada próxima linha de um conjunto de resultados do Sybase deve ser igual para a próxima linha do conjunto de resultados gerado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Você pode editar essas instruções SELECT para fornecer verificação personalizada. Para salvar as alterações no Sybase e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instruções, use o **aplicar** botões na origem e de destino SQL, de forma correspondente.  
  
## <a name="next-step"></a>Próxima etapa  
[Personalizando a ordem de chamadas &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Casos de teste de execução &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Teste de objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
