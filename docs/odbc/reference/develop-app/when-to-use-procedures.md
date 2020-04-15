---
title: Quando usar procedimentos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31aeea226bc8c8aa41f748d1d9a97d55147c4d67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289093"
---
# <a name="when-to-use-procedures"></a>Quando usar procedimentos
Há uma série de vantagens no uso de procedimentos, tudo baseado no fato de que o uso de procedimentos move as declarações SQL do aplicativo para a fonte de dados. O que resta na aplicação é uma chamada de procedimento interoperável. Essas vantagens incluem:  
  
-   **Desempenho** Os procedimentos geralmente são a maneira mais rápida de executar declarações SQL. Como execução preparada, a declaração é compilada e executada em duas etapas distintas. Ao contrário da execução preparada, os procedimentos são executados apenas em tempo de execução. Eles são compilados em um momento diferente.  
  
-   **Regras de negócios** Uma *regra de negócios* é uma regra sobre a forma como uma empresa faz negócios. Por exemplo, apenas alguém com o título Sales Person pode ser autorizado a adicionar novas ordens de venda. A colocação dessas regras em procedimentos permite que empresas individuais personalizem aplicações verticais reescrevendo os procedimentos chamados pelo aplicativo sem ter que modificar o código do aplicativo. Por exemplo, um aplicativo de entrada de pedidos pode chamar o procedimento **InsertOrder** com um número fixo de parâmetros; exatamente como **o InsertOrder** é implementado pode variar de empresa para empresa.  
  
-   **Capacidade de substituição** Intimamente relacionado à colocação de regras de negócios em procedimentos é o fato de que os procedimentos podem ser substituídos sem recompilar o aplicativo. Se uma regra de negócio mudar após uma empresa comprar e instalar um aplicativo, a empresa pode alterar o procedimento que contém essa regra. Do ponto de vista do aplicativo, nada mudou; ele ainda chama um procedimento específico para realizar uma tarefa específica.  
  
-   **SQL específico do DBMS** Os procedimentos fornecem uma maneira de os aplicativos explorarem o SQL específico do DBMS e ainda permanecem interoperáveis. Por exemplo, um procedimento em um DBMS que suporta instruções de controle de fluxo no SQL pode prender e recuperar de erros, enquanto um procedimento em um DBMS que não suporta instruções de controle de fluxo pode simplesmente retornar um erro.  
  
-   **Procedimentos sobrevivem a transações** Em algumas fontes de dados, os planos de acesso para todas as declarações preparadas em uma conexão são excluídos quando uma transação é cometida ou revertida. Ao colocar as declarações SQL em procedimentos, que são permanentemente armazenados na fonte de dados, as declarações sobrevivem à transação. Se os procedimentos sobrevivem em um estado preparado, parcialmente preparado ou despreparado é específico do DBMS.  
  
-   **Desenvolvimento separado** Os procedimentos podem ser desenvolvidos separadamente do resto da aplicação. Em grandes corporações, isso pode fornecer uma maneira de explorar ainda mais as habilidades de programadores altamente especializados. Em outras palavras, os programadores de aplicativos podem escrever código de interface de usuário e programadores de banco de dados podem escrever procedimentos.  
  
 Os procedimentos são geralmente usados por aplicações verticais e personalizadas. Esses aplicativos tendem a executar tarefas fixas, e é possível fazer chamadas de procedimento de código rígido neles. Por exemplo, um aplicativo de entrada de pedidos pode chamar os procedimentos **InsertOrder,** **DeleteOrder,** **UpdateOrder**e **GetOrders**.  
  
 Há pouca razão para chamar procedimentos de aplicações genéricas. Os procedimentos geralmente são escritos para executar uma tarefa no contexto de um determinado aplicativo e, portanto, não têm uso para aplicativos genéricos. Por exemplo, uma planilha não tem razão para chamar o procedimento **InsertOrder** mencionado. Além disso, os aplicativos genéricos não devem construir procedimentos em tempo de execução na esperança de fornecer uma execução mais rápida da declaração; não só é provável que isso seja mais lento do que a execução direta ou preparada, mas também requer declarações SQL específicas do DBMS.  
  
 Uma exceção a isso são os ambientes de desenvolvimento de aplicativos, que muitas vezes fornecem uma maneira para os programadores construirem instruções SQL que executam procedimentos e podem fornecer uma maneira para os programadores testarem procedimentos. Esses ambientes chamam **sqlprocedures** para listar procedimentos disponíveis e **SQLProcedureColumns** para listar os parâmetros de entrada, entrada/saída e saída, o valor de retorno do procedimento e as colunas de quaisquer conjuntos de resultados criados por um procedimento. No entanto, tais procedimentos devem ser desenvolvidos previamente em cada fonte de dados; fazê-lo requer instruções SQL específicas do DBMS.  
  
 Há três grandes desvantagens no uso de procedimentos. A primeira é que os procedimentos devem ser escritos e compilados para cada DBMS com o qual o aplicativo deve ser executado. Embora isso não seja um problema para aplicações personalizadas, ele pode aumentar significativamente o tempo de desenvolvimento e manutenção para aplicações verticais projetadas para serem executadas com uma série de DBMSs.  
  
 A segunda desvantagem é que muitos DBMSs não suportam procedimentos. Mais uma vez, é mais provável que este seja um problema para aplicações verticais projetadas para serem executadas com um número de DBMSs. Para determinar se os procedimentos são suportados, um aplicativo chama **sqlGetInfo** com a opção SQL_PROCEDURES.  
  
 A terceira desvantagem, que é particularmente aplicável aos ambientes de desenvolvimento de aplicativos, é que a ODBC não define uma gramática padrão para a criação de procedimentos. Ou seja, embora os aplicativos possam chamar procedimentos interperavelmente, eles não podem criá-los interperavelmente.
