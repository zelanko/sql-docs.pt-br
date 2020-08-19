---
description: Preparar e executar comandos
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 19539844381f38de4700925a0ecdbc0f8e74fb0d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453028"
---
# <a name="preparing-and-executing-commands"></a>Preparar e executar comandos
Comandos são instruções emitidas para um provedor para executar algumas operações na fonte de dados subjacente. Uma instrução SQL, por exemplo, é um comando para o Microsoft SQL Provedor de Dados. No ADO, os comandos são normalmente representados por objetos de **comando** , embora comandos simples também possam ser emitidos por meio de objetos de **conexão** ou **conjunto de registros** .  
  
 Você pode usar o objeto de **comando** para solicitar qualquer tipo de operação com suporte do provedor, supondo que o provedor possa interpretar a cadeia de caracteres de comando corretamente. Uma operação comum para provedores de dados é consultar um banco de dado e retornar registros em um objeto **Recordset** , que pode ser considerado um contêiner para manter o resultado e uma ferramenta para exibir o resultado. Assim como ocorre com muitos objetos ADO, algumas coleções de objetos de **comando** , métodos ou propriedades podem gerar erros quando referenciados, dependendo da funcionalidade do provedor.  
  
 Além de usar objetos de **comando** , você pode usar o método **Execute** no objeto **Connection** ou o método **Open** no objeto **Recordset** para emitir um comando e executá-lo. No entanto, você deve usar um objeto de **comando** se precisar reutilizar um comando em seu código ou se precisar passar informações de parâmetro detalhadas com o comando. Esses cenários são abordados em mais detalhes posteriormente nesta seção.  
  
> [!NOTE]
>  Determinados s de **comando**podem retornar um conjunto de resultados como um fluxo binário ou um único **registro** em vez de como um **conjunto de registros**, se houver suporte para ele no provedor. Além disso, alguns s de **comando**não se destinam a retornar qualquer conjunto de resultados (por exemplo, uma consulta SQL Update). Esta seção abordará o cenário mais típico, no entanto: executando o **comando**s que retornam resultados como um objeto **Recordset** . Para obter mais informações sobre como retornar resultados no **registro**s ou no **Stream**s, consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Visão geral do objeto Command](../../../ado/guide/data/command-object-overview.md)  
  
-   [Criar e executar um comando simples](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Parâmetros do objeto Command](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Chamando um procedimento armazenado com um comando](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Chamando um procedimento armazenado como um método em um objeto de conexão](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Comandos nomeados](../../../ado/guide/data/named-commands.md)  
  
-   [Passar parâmetros para um comando nomeado](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
