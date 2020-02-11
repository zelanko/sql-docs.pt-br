---
title: Selecionando e configurando objetos a serem testados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2951d4c3bf1eae73ffd066d796b0e3dda4d28cf6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020957"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Selecionar e configurar os objetos a testar (SybaseToSQL)
Nesta etapa, você seleciona os objetos a serem testados e define as configurações para comparar os parâmetros de saída dos procedimentos e das funções, bem como os valores de retorno das funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos a serem testados  
Na árvore de objetos do Sybase localizada no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos que podem ser testados no tópico [testando objetos de banco de dados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) .  
  
Se o SSMA Tester não oferecer suporte a nenhum dos objetos selecionados para teste, você verá que o link rotulado **alguns objetos selecionados contém erros** na árvore de objetos. Clique neste link para exibir os motivos pelos quais esses objetos não podem ser testados e para limpar a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas a página **SQL** mostra a definição do objeto atual. Nas páginas **pre SQL** e **post SQL** podem especificar scripts que são executados antes e depois que a invocação do objeto de teste é iniciada. Isso pode ser útil quando o objeto requer um objeto adicional, tais como tabelas temporárias ou cursores. A página **parâmetros** lista os parâmetros se o objeto for um procedimento armazenado ou uma função. A página **Propriedades** mostra características adicionais do objeto. Consulte a descrição das páginas de **análise de parâmetros** e **valores de chamada** abaixo.  
  
## <a name="parameter-comparison-settings"></a>Configurações de comparação de parâmetros  
Estabeleça as regras de comparação para os parâmetros de saída e valores de retorno na página **parâmetros de comparação** . Você pode fazer as seguintes configurações.  
  
### <a name="use-during-comparisons"></a>Usar durante comparações  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **true**, o SSMA comparará o valor de saída desse parâmetro depois de executar o procedimento no Sybase com o valor correspondente em[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Se você escolher**false**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numérico aproximado e de comprimento fixo, você pode definir uma escala personalizada para a comparação.  
  
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
Você pode especificar valores de parâmetro de entrada na página **valores de chamada** . O botão **Adicionar chamada** adiciona uma nova chamada com valores de parâmetro vazios. O botão **remover chamada** remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionando e configurando objetos afetados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Testando objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
