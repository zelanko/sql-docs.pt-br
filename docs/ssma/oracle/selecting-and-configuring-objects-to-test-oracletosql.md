---
title: Selecionando e Configurando objetos a testar (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: e0a8e7650534d50c5e5d7c3b02f2857764d9c2ca
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264636"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Selecionar e configurar os objetos a testar (OracleToSQL)
Nesta etapa, você seleciona objetos a testar e definir as configurações para comparar procedimentos e dos funções parâmetros de saída, bem como os valores de retorno de funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos para teste  
Na árvore de objetos de Oracle localizado no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos que podem ser testados na [testes migrados de objetos de banco de dados &#40;OracleToSQL&#41; ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) tópico.  
  
Se o testador SSMA não oferece suporte a qualquer um dos objetos selecionados para teste, você verá o link rotulado **alguns objetos selecionados contêm erros** abaixo da árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser testados e desmarque a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas de **SQL** página mostra a definição do objeto atual. O **parâmetros** página lista os parâmetros se o objeto for um procedimento armazenado ou uma função. O **propriedades** página mostra as características adicionais do objeto. Consulte a descrição da **parâmetro comparações** e **chamar valores** páginas abaixo.  
  
## <a name="parameter-comparison-settings"></a>Configurações de comparação de parâmetro  
Estabelecer as regras de comparação para parâmetros de saída e retornar valores de **comparações de parâmetro** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Use durante as comparações de teste  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **verdadeira**, SSMA irá comparar o valor desse parâmetro de saída após executar o procedimento no Oracle com o valor correspondente no SQL Server.
  
-   Se você escolher**falsos**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numérico, você pode definir um dimensionamento personalizado para a comparação.  
  
-   Se você escolher **verdadeira**, valores numéricos serão arredondados de acordo com o **comparando escala** valor antes de serem comparadas.  
  
-   Se você escolher**falsos**, a comparação numérica será ser exata.  
  
### <a name="comparing-scale"></a>Comparação de escala  
Disponível somente se o **escala personalizada de uso** opção for definida como **verdadeiro**. Isso é a precisão de comparação numérica.  
  
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
  
-   Se você escolher **falsos**, a comparação será diferencia maiusculas de minúsculas.  
  
### <a name="ignore-trailing-spaces"></a>Ignorar Espaços à Direita  
Controla os espaços à direita como são tratados durante a comparação.  
  
-   Se você escolher **verdadeira**, em comparação com as cadeias de caracteres será cortado para direita antes de comparar.  
  
-   Se você escolher **falsos**, em comparação com as cadeias de caracteres irá preservar espaço em branco à direita.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Especificar valores de entrada para procedimentos e funções (valores de chamada)  
Você pode especificar valores de parâmetro de entrada sobre o **chamar valores** página. O **adicionar chamar** botão adiciona uma nova chamada com os valores de parâmetros vazia. O **remover chamadas** botão remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionar e configurar os objetos afetados pelo &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Testar objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
