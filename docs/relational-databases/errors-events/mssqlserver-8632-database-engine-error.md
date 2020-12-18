---
description: MSSQLSERVER_8632
title: MSSQLSERVER_8632
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8632 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 36f8b6f7eb55a30becf0f56eb318c6740b5783ec
ms.sourcegitcommit: f87f2f0f1edc91fe400040d8e3a5810347aa8d70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96868892"
---
# <a name="mssqlserver_8632"></a>MSSQLSERVER_8632
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|8632|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|QUERY_EXPRESSION_TOO_COMPLEX|
|Texto da mensagem|Erro interno: um limite dos serviços de expressão foi atingido. Procure expressões complexas na consulta e tente simplificá-las.|
||

## <a name="explanation"></a>Explicação

O erro 8632 é gerado quando você executa uma consulta em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém um grande número de identificadores e constantes em uma só expressão. Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> Servidor:  Mensagem 8632, Nível 17, Estado 2, Linha 1  
Erro interno: um limite dos serviços de expressão foi atingido. Procure expressões complexas na consulta e tente simplificá-las.

## <a name="cause"></a>Causa

Isso ocorre porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] limita o número de identificadores e de constantes que podem ser contidos em uma única expressão de uma consulta. Esse limite é de 65.535. Por exemplo, a seguinte consulta tem apenas uma expressão:

```sql
select a, b + c, d + e
```

Essa expressão recupera as cinco colunas, calcula os operadores de adição e envia três resultados projetados para o cliente.

O teste para o número de identificadores e constantes é executado depois que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] expande todos os identificadores e constantes referenciados. Por exemplo, os seguintes itens podem ser expandidos:

- O asterisco (*) na lista de seleção
- Uma exibição
- Uma definição de coluna computada

Se o número após a expansão exceder o limite, a consulta não poderá ser executada.

## <a name="user-action"></a>Ação do usuário

Para contornar esse problema, reescreva a consulta. Referencie menos identificadores e constantes na expressão maior da consulta. O número de identificadores e constantes em cada expressão da consulta não deve exceder o limite. Para isso, talvez seja necessário dividir uma consulta em mais de uma. Em seguida, crie um resultado intermediário temporário.
