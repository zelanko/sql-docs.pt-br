---
title: Selecionando e configurando objetos a serem testados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: fd5a65e50889d461b0922fa255680a76863ca0a4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932757"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Selecionar e configurar os objetos a testar (OracleToSQL)
Nesta etapa, você seleciona os objetos a serem testados e define as configurações para comparar os parâmetros de saída dos procedimentos e das funções, bem como os valores de retorno das funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos a serem testados  
Na árvore de objetos do Oracle, localizada no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos que podem ser testados no tópico [testando objetos de banco de dados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) .  
  
Se o SSMA Tester não oferecer suporte a nenhum dos objetos selecionados para teste, você verá que o link rotulado **alguns objetos selecionados contém erros** na árvore de objetos. Clique neste link para exibir os motivos pelos quais esses objetos não podem ser testados e para limpar a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas a página **SQL** mostra a definição do objeto atual. A página **parâmetros** lista os parâmetros se o objeto for um procedimento armazenado ou uma função. A página **Propriedades** mostra características adicionais do objeto. Consulte a descrição das páginas **comparações de parâmetro** e **valores de chamada** abaixo.  
  
## <a name="parameter-comparison-settings"></a>Configurações de comparação de parâmetros  
Estabeleça as regras de comparação para parâmetros de saída e valores de retorno na página **comparações de parâmetro** . Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Usar durante comparações de teste  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **true**, o SSMA comparará o valor de saída desse parâmetro depois de executar o procedimento no Oracle com o valor correspondente em SQL Server.
  
-   Se você escolher**false**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numéricos, você pode definir uma escala personalizada para a comparação.  
  
-   Se você escolher **true**, os valores numéricos serão arredondados de acordo com o valor de **escala de comparação** antes de serem comparados.  
  
-   Se você escolher**false**, a comparação numérica será exata.  
  
### <a name="comparing-scale"></a>Comparando escala  
Disponível somente se a opção **usar escala personalizada** estiver definida como **true**. Essa é a precisão para comparação numérica.  
  
### <a name="date-time-comparing"></a>Comparação de data e hora  
Define como os valores de data/hora são comparados.  
  
-   Se você selecionar **comparar data inteira**, a comparação completa de valores de ambas as plataformas será executada.  
  
-   Se você selecionar **comparar somente data**, a parte de hora será ignorada.  
  
-   Se você selecionar **comparar apenas hora**, a parte de data será ignorada.  
  
-   Se você selecionar **ignorar milissegundos**, os resultados serão comparados a até segundos.  
  
-   Se você selecionar **ignorar data e milissegundos**, o resultado será comparado apenas por parte do tempo e ignorando partes fracionárias de um segundo.  
  
### <a name="ignore-strings-case"></a>Ignorar caso de cadeia de caracteres  
Controla a sensibilidade do caso de comparação.  
  
-   Se você escolher **true**, a comparação não diferenciará maiúsculas de minúsculas.  
  
-   Se você escolher **false**, a comparação será diferenciada entre maiúsculas e minúsculas.  
  
### <a name="ignore-trailing-spaces"></a>Ignorar Espaços à Direita  
Controla como os espaços à direita são tratados durante a comparação.  
  
-   Se você escolher **true**, as cadeias de caracteres comparadas serão cortadas com o botão direito do mouse antes de comparar.  
  
-   Se você escolher **false**, as cadeias de caracteres comparadas preservarão o espaço em branco à direita.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Especificar valores de entrada para procedimentos e funções (valores de chamada)  
Você pode especificar valores de parâmetro de entrada na página **valores de chamada** . O botão **Adicionar chamada** adiciona uma nova chamada com valores de parâmetro vazios. O botão **remover chamadas** remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionando e configurando objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
