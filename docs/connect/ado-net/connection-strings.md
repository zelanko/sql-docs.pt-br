---
title: Cadeias de conexão
description: Saiba mais sobre cadeias de conexão no Provedor de Dados Microsoft SqlClient para SQL Server, que contêm informações de inicialização passadas como um parâmetro de um provedor de dados para uma fonte de dados.
ms.date: 11/13/2020
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e37d77304644d1adb50bb195dd32d4c4e1222c09
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126332"
---
# <a name="connection-strings-in-adonet"></a>Cadeias de conexão no ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Uma cadeia de conexão contém informações de inicialização que são passadas como parâmetros de um provedor de dados para uma fonte de dados. O provedor de dados recebe a cadeia de conexão como o valor da propriedade <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType>. O provedor analisa a cadeia de conexão, garantindo que a sintaxe esteja correta e que as palavras-chave tenham suporte. Em seguida, o método <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> passa os parâmetros de conexão analisados para a fonte de dados. A fonte de dados executa uma validação adicional e estabelece uma conexão.

## <a name="connection-string-syntax"></a>Sintaxe de cadeia de conexão

A cadeia de conexão é uma lista de pares chave-valor de parâmetros separados por ponto e vírgula:

```csharp
keyword1=value; keyword2=value;
```

As palavras-chave não diferenciam maiúsculas de minúsculas. Os valores, no entanto, podem diferenciar maiúsculas de minúsculas, dependendo da fonte de dados. As palavras-chave e os valores podem conter [caracteres de espaço em branco](https://en.wikipedia.org/wiki/Whitespace_character#Unicode). Espaços em branco à esquerda e à direita são ignorados em palavras-chave e valores sem aspas.

Se um valor contiver o ponto e vírgula, [caracteres de controle Unicode](https://en.wikipedia.org/wiki/Unicode_control_characters)ou espaços em branco à esquerda ou à direita, ele deverá ser colocado entre aspas simples ou duplas. Por exemplo:

```csharp
Keyword=" whitespace  ";
Keyword='special;character';
```

O caractere delimitador pode não ocorrer dentro do valor que ele inclui. Portanto, um valor contendo aspas simples pode ser colocado somente entre aspas duplas, e vice-versa:

```csharp
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

Você também pode fazer escape do caractere delimitador usando os dois tipos de aspas juntos:

```csharp
Keyword="double""quotation";
Keyword='single''quotation';
```

As aspas em si, bem como o sinal de igual, não exigem escape, portanto, as seguintes cadeias de conexão são válidas:

```csharp
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

Como cada valor é lido até o próximo ponto e vírgula ou o final da cadeia de caracteres, o valor no último exemplo é `a=b=c`, e o ponto e vírgula final é opcional.

Todas as cadeias de conexão compartilham a mesma sintaxe básica descrita acima. O conjunto de palavras-chave reconhecidas depende do provedor. O provedor de dados *Microsoft SqlClient* para *SQL Server* dá suporte a muitas palavras-chave de APIs mais antigas, mas é geralmente mais flexível e aceita sinônimos para muitas das palavras-chave comuns da cadeia de conexão.

Erros de digitação podem causar problemas. Por exemplo, `Integrated Security=true` é válido, mas `IntegratedSecurity=true` gera um erro.

As cadeias de conexão construídas manualmente em tempo de execução a partir de uma entrada de usuário não validada são vulneráveis a ataques de injeção de cadeia de caracteres, colocando em risco a segurança da fonte de dados. Para resolver esses problemas, o [construtor de cadeias de conexão](connection-string-builders.md) foi criado. Esse construtor expõe parâmetros como propriedades fortemente tipadas e torna possível validar a cadeia de conexão antes que ela seja enviada para a fonte de dados.

## <a name="in-this-section"></a>Nesta seção

[Construtor de cadeia de conexão](connection-string-builders.md)\
Demonstra como usar a classe `ConnectionStringBuilder` para construir cadeias de conexão válidas em tempo de execução.

[Cadeias de conexão e arquivos de configuração](connection-strings-and-configuration-files.md)\
Demonstra como armazenar e recuperar cadeias de conexão em arquivos de configuração.

[Sintaxe de cadeia de conexão](connection-string-syntax.md)\
Descreve como configurar cadeias de conexão específicas do provedor para `SqlClient`.

[Proteger informações de conexão](protecting-connection-information.md)\
Demonstra técnicas para proteger informações usadas para se conectar a uma fonte de dados.
