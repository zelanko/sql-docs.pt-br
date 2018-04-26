---
title: Selecionando e Configurando objetos para teste (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26d6e9d0a07ddc32f20c80f3d0d476131721d969
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>Selecionando e Configurando objetos para teste (SybaseToSQL)
Nesta etapa, você seleciona objetos a testar e definir configurações para a comparação dos procedimentos e dos funções parâmetros de saída, bem como os valores de retorno de funções.  
  
## <a name="selection-of-objects-to-test"></a>Seleção de objetos para teste  
Na árvore de objetos de Sybase localizado no lado esquerdo da janela, verifique os objetos que você deseja invocar durante o processo de teste. Consulte a lista completa de objetos podem ser testados no [teste objetos de banco de dados migrados &#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md) tópico.  
  
Se o SSMA Tester não dá suporte a qualquer um dos objetos selecionados para teste, você verá o link rotulado **alguns objetos selecionados contêm erros** na árvore de objetos. Clique neste link para exibir as razões por que esses objetos não podem ser testados e desmarque a seleção de objetos errados.  
  
No lado direito, você pode exibir várias páginas de **SQL** página mostra a definição do objeto atual. No **Pre SQL** e **Post SQL** páginas podem especificar scripts que são executados antes e depois da invocação do início do objeto de teste. É por isso pode ser útil quando o objeto requer objetos adicionais, essas tabelas temporárias ou cursores. O **parâmetros** página lista os parâmetros se o objeto for um procedimento armazenado ou uma função. O **propriedades** página mostra as características adicionais do objeto. Consulte a descrição do **parâmetros Comparsions** e **valores chamar** páginas abaixo.  
  
## <a name="parameter-comparison-settings"></a>Parâmetros de comparação  
Estabelecer as regras de comparação para parâmetros de saída e valores de retorno de **parâmetros comparando** página. Você pode fazer as seguintes configurações.  
  
### <a name="use-during-comparisons"></a>Use durante as comparações  
Habilite o uso do parâmetro selecionado na comparação de resultados de teste.  
  
-   Se você escolher **True**, SSMA irá comparar o valor desse parâmetro de saída depois de executar o procedimento em Sybase com o valor correspondente em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Se você escolher**False**, o parâmetro será excluído da verificação de resultados.  
  
### <a name="use-custom-scale"></a>Usar escala personalizada  
Para parâmetros de tipo de dados numéricos de comprimento fixo e aproximado, você pode definir uma escala personalizada para a comparação.  
  
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
Você pode especificar valores de parâmetro de entrada no **valores chamar** página. O **adicionar chamar** botão adiciona uma nova chamada com valores de parâmetros vazia. O **remover chamar** botão remove a chamada atual.  
  
## <a name="next-step"></a>Próxima etapa  
[Selecionar e configurar objetos afetados &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Teste de objetos de banco de dados migrados &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
