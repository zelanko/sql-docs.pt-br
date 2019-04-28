---
title: Selecionando e Configurando objetos a testar (SybaseToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2b8d842e9febc94d35f2a8c53c6106159f44423a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667434"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Selecionar e configurar os objetos a testar (SybaseToSQL)
Nesta etapa, você seleciona objetos a testar e definir as configurações para comparar procedimentos e dos funções parâmetros de saída, bem como os valores de retorno de funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos para teste  
Na árvore de objeto do Sybase localizado no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos que podem ser testados na [testes migrados de objetos de banco de dados &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) tópico.  
  
Se o testador SSMA não oferece suporte a qualquer um dos objetos selecionados para teste, você verá o link rotulado **alguns objetos selecionados contêm erros** abaixo da árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser testados e desmarque a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas de **SQL** página mostra a definição do objeto atual. No **SQL pré** e **Post SQL** páginas podem especificar scripts que são executados antes e depois da chamada de inícios de objeto de teste. É por isso pode ser útil quando o objeto requer objeto adicionais, como tabelas temporárias ou cursores. O **parâmetros** página lista os parâmetros se o objeto for um procedimento armazenado ou uma função. O **propriedades** página mostra as características adicionais do objeto. Consulte a descrição da **parâmetros Comparsions** e **chamar valores** páginas abaixo.  
  
## <a name="parameter-comparison-settings"></a>Configurações de comparação de parâmetro  
Estabelecer as regras de comparação para parâmetros de saída e retornar valores na **parâmetros de comparação** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-comparisons"></a>Use durante as comparações  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **verdadeira**, SSMA irá comparar o valor desse parâmetro de saída após executar o procedimento em sistemas Sybase com o valor correspondente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Se você escolher**falsos**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numéricos de comprimento fixo e aproximado, você pode definir um dimensionamento personalizado para a comparação.  
  
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
Você pode especificar valores de parâmetro de entrada sobre o **chamar valores** página. O **adicionar chamar** botão adiciona uma nova chamada com os valores de parâmetros vazia. O **remover chamar** botão remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionar e configurar os objetos afetados pelo &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Testar objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
