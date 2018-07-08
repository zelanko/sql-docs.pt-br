---
title: Transações do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4002487af9dba5e4466b75e3fce19ce0c9b8d531
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165007"
---
# <a name="integration-services-transactions"></a>Transações do Integration Services
  Os pacotes usam transações para associar as ações do banco de dados realizadas pelas tarefas em unidades atômicas e, ao fazer isso, a integridade dos dados é mantida. Todos os tipos de contêineres do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , pacotes, o Loop For, Loop Foreach, contêineres de Sequência, e os hosts de tarefas que encapsulam cada tarefa, podem ser configurados para usar transações. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece três opções para configurar transações: **Sem Suporte**, **Há Suporte**e **Necessário**.  
  
-   **Necessário** indica que o contêiner inicia uma transação, a menos que uma já tenha sido iniciada por seu contêiner pai. Se uma transação já existir, o contêiner se unirá à transação. Por exemplo, se um pacote que não está configurado para dar suporte a transações incluísse um contêiner Sequência que usa a opção **Necessário** , o contêiner iniciaria sua própria transação. Se o pacote fosse configurado para usar a opção **Necessário** , o contêiner Sequência se uniria à transação do pacote.  
  
-   **Há Suporte** indica que o contêiner não inicia uma transação, mas se une a qualquer transação iniciada por seu contêiner pai. Por exemplo, se um pacote com quatro tarefas Executar SQL iniciar uma transação e todas as quatro tarefas usarem a opção **Há Suporte** , as atualizações de banco de dados realizadas pelas tarefas Executar SQL serão revertidas se qualquer tarefa falhar. Se o pacote não iniciar uma transação, as quatro tarefas Executar SQL não serão associadas por uma transação e nenhuma atualização de banco de dados, exceto as realizadas pela tarefa que falhou, será revertida.  
  
-   **Sem Suporte** indica que o contêiner não inicia uma transação ou se une a uma transação existente. Uma transação iniciada por um contêiner pai não afeta contêineres filhos que foram configurados para não suportar transações. Por exemplo, se um pacote for configurado para iniciar uma transação e um contêiner Loop For no pacote usar a opção **Sem Suporte** , nenhuma das tarefas no Loop For poderão ser revertidas se falharem.  
  
 Você configura transações definindo a propriedade TransactionOption no contêiner. É possível definir essa propriedade na janela **Propriedades** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ou definir a propriedade programaticamente.  
  
> [!NOTE]  
>  A propriedade `TransactionOption` influencia a aplicação ou não do valor da propriedade `IsolationLevel` solicitada por um contêiner. Para obter mais informações, consulte a descrição do `IsolationLevel` propriedade no tópico [definindo propriedades do pacote](set-package-properties.md).  
  
### <a name="to-configure-a-package-to-use-transactions"></a>Para configurar um pacote para usar transações  
  
-   [Configurar um pacote para usar transações](../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [How to Use Transactions in SQL Server Integration Services SSIS (em inglês)](http://go.microsoft.com/fwlink/?LinkId=157783), em www.mssqltips.com  
  
## <a name="see-also"></a>Consulte também  
 [Transações herdadas](../../2014/integration-services/inherited-transactions.md)   
 [Transações múltiplas](../../2014/integration-services/multiple-transactions.md)  
  
  
