---
title: Preparando e executando comandos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f3de2bb729e2096e1b30aab12c402803036914b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911355"
---
# <a name="preparing-and-executing-commands"></a>Preparar e executar comandos
Comandos são emitidas para um provedor de instruções para executar algumas operações na fonte de dados subjacente. Uma instrução SQL, por exemplo, é um comando para o provedor de dados do Microsoft SQL. No ADO, comandos normalmente são representados por **comando** objetos, embora simples comandos também podem ser emitidos por meio **Conexão** ou **Recordset** objetos.  
  
 Você pode usar o **comando** objeto solicitar qualquer tipo com suporte de operação do provedor, supondo que o provedor pode interpretar corretamente a cadeia de caracteres de comando. Uma operação comum para provedores de dados é um banco de dados e retornar registros em uma **Recordset** objeto, que pode ser pensado como um contêiner para armazenar o resultado e uma ferramenta para exibir o resultado. Assim como acontece com muitos objetos do ADO, alguns **comando** coleções de objetos, métodos ou propriedades podem gerar erros quando referenciado, dependendo da funcionalidade do provedor.  
  
 Além de usar **comando** objetos, você pode usar o **Execute** método no **Conexão** objeto ou o **abrir** método sobre o  **Conjunto de registros** objeto para emitir um comando e que ele seja executado. No entanto, você deve usar um **comando** caso você precise reutilizar um comando em seu código, ou se você precisar passar informações de parâmetro detalhadas com o comando do objeto. Esses cenários são abordados em mais detalhes posteriormente nesta seção.  
  
> [!NOTE]
>  Determinados **comando**s podem retornar um resultado definido como um fluxo binário ou como uma única **registro** em vez de como um **Recordset**, se isso for suportado pelo provedor. Além disso, alguns **comando**s não devem retornar qualquer resultado definido em todos os (por exemplo, uma consulta de atualização do SQL). Esta seção abordará o cenário mais comum, porém: executar **comando**s que retornam resultados como um **Recordset** objeto. Para obter mais informações sobre como retornar resultados para o **registro**s ou **Stream**s, consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Visão geral do objeto Command](../../../ado/guide/data/command-object-overview.md)  
  
-   [Criando e executando um comando simples](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Parâmetros do objeto Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Chamando um procedimento armazenado com um comando](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Chamar um procedimento armazenado como um método em um objeto de Conexão](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Comandos nomeados](../../../ado/guide/data/named-commands.md)  
  
-   [Passando parâmetros para um comando nomeado](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
