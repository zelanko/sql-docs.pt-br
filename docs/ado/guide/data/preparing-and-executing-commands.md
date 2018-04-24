---
title: Preparar e executar comandos | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfe5be8b68fe701d5b44431ab6e10cf8445deda3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="preparing-and-executing-commands"></a>Preparação e execução de comandos
Comandos são emitidas para um provedor de instruções para executar algumas operações em relação à fonte de dados subjacente. Uma instrução SQL, por exemplo, é um comando para o provedor de dados do Microsoft SQL. No ADO, comandos normalmente são representados por **comando** objetos, embora simples comandos também podem ser emitidos por **Conexão** ou **registros** objetos.  
  
 Você pode usar o **comando** objeto solicitar qualquer tipo de operação do provedor, supondo que o provedor pode interpretar a cadeia de caracteres de comando corretamente. É uma operação comum para provedores de dados consultar um banco de dados e retornar os registros em um **registros** objeto que pode ser pensado como um contêiner para armazenar o resultado e uma ferramenta para exibir o resultado. Assim como acontece com muitos objetos ADO, alguns **comando** coleções de objetos, métodos ou propriedades podem gerar erros quando referenciada, dependendo da funcionalidade do provedor.  
  
 Além de usar **comando** objetos, você pode usar o **Execute** método no **Conexão** objeto ou o **abrir** método sobre o  **Conjunto de registros** objeto para emitir um comando e que ele seja executado. No entanto, você deve usar um **comando** objeto se for necessário reutilizar um comando no seu código, ou se você precisar passar informações detalhadas de parâmetro com o comando. Esses cenários são abordados em mais detalhes posteriormente nesta seção.  
  
> [!NOTE]
>  Determinados **comando**s pode retornar um resultado definido como um fluxo binário ou como um único **registro** em vez de como um **registros**, se isso for suportado pelo provedor. Além disso, alguns **comando**s não devem retornar qualquer em todos os conjunto de resultados (por exemplo, uma consulta de atualização do SQL). Esta seção aborda o cenário mais comum, porém: executar **comando**que retornam resultados como um **registros** objeto. Para obter mais informações sobre como retornar resultados **registro**s ou **fluxo**s, consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Visão geral do objeto Command](../../../ado/guide/data/command-object-overview.md)  
  
-   [Criando e executando um comando simples](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Parâmetros do objeto Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Chamando um procedimento armazenado com um comando](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Chamar um procedimento armazenado como um método em um objeto de Conexão](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Comandos nomeados](../../../ado/guide/data/named-commands.md)  
  
-   [Passando parâmetros para um comando nomeado](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
