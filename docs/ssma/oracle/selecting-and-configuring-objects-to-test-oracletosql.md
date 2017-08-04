---
title: Selecionando e Configurando objetos para teste (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b12a1b9ec20f736072d57039d247be13be57e69
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>Selecionando e Configurando objetos para teste (OracleToSQL)
Nesta etapa, você seleciona objetos a testar e definir configurações para a comparação dos procedimentos e dos funções parâmetros de saída, bem como os valores de retorno de funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos para teste  
Na árvore de objetos de Oracle localizado no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos podem ser testados no [teste objetos migrados do banco de dados &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) tópico.  
  
Se o SSMA Tester não dá suporte a qualquer um dos objetos selecionados para teste, você verá o link rotulado **alguns objetos selecionados contêm erros** na árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser testados e desmarque a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas de **SQL** página mostra a definição do objeto atual. O **parâmetros** página lista os parâmetros se o objeto for um procedimento armazenado ou uma função. O **propriedades** página mostra as características adicionais do objeto. Consulte a descrição do **parâmetro comparações** e **valores chamar** páginas abaixo.  
  
## <a name="parameter-comparison-settings"></a>Parâmetros de comparação  
Estabelecer as regras de comparação para parâmetros de saída e valores de retorno de **parâmetro comparações** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-test-comparisons"></a>Use durante as comparações de teste  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **True**, SSMA irá comparar o valor desse parâmetro de saída depois de executar o procedimento no Oracle com o valor correspondente no SQL Server.
  
-   Se você escolher**False**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numérico, você pode definir uma escala personalizada para a comparação.  
  
-   Se você escolher **True**, valores numéricos serão arredondados de acordo com o **comparando escala** valor antes de serem comparadas.  
  
-   Se você escolher**False**, a comparação numérica será exata.  
  
### <a name="comparing-scale"></a>Comparação de escala  
Disponível somente se o **escala personalizada de uso** opção é definida como **True**. Isso é a precisão para comparação numérica.  
  
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
  
-   Se você escolher **False**, a comparação será entre maiusculas e minúsculas.  
  
### <a name="ignore-trailing-spaces"></a>Ignorar Espaços à Direita  
Controla os espaços à direita como são tratados durante a comparação.  
  
-   Se você escolher **True**, em comparação com as cadeias de caracteres serão cortados direita antes de comparar.  
  
-   Se você escolher **False**, em comparação com as cadeias de caracteres irá preservar espaço em branco à direita.  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>Especificar valores de entrada para procedimentos e funções (valores de chamada)  
Você pode especificar valores de parâmetro de entrada no **valores chamar** página. O **adicionar chamar** botão adiciona uma nova chamada com valores de parâmetros vazia. O **remover chamadas** botão remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionando e configurando afetados objetos &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Testando migrados objetos de banco de dados &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

