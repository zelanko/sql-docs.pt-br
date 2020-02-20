---
title: Noções básicas sobre as diferenças de tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 906a4abf0768fcad2e5ac31a0ee93345dcc8b30c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027377"
---
# <a name="understanding-data-type-differences"></a>Entendendo diferenças de tipo de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Há várias diferenças entre os tipos de dados da linguagem de programação Java e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ajuda a facilitar essas diferenças por meio de vários tipos de conversões.  

## <a name="character-types"></a>Tipos de caracteres

Os tipos de dados da cadeia de caracteres JDBC são **CHAR**, **VARCHAR** e **LONGVARCHAR**. O driver JDBC oferece suporte à API do JDBC 4.0. No JDBC 4.0, os tipos de dados da cadeia de caracteres JDBC também podem ser **NCHAR**, **NVARCHAR** e **LONGNVARCHAR**. Estes novos tipos de cadeia de caracteres mantêm tipos de caracteres nativos de Java em formato Unicode e remove a necessidade de executar alguma conversão ANSI-para-Unicode ou Unicode-para-ANSI.  
  
| Type            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Comprimento fixo    | Os tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char** e **nchar** são mapeados diretamente para os tipos **CHAR** e **NCHAR** do JDBC. São tipos de comprimentos fixos com preenchimento fornecidos pelo servidor caso a coluna tenha `SET ANSI_PADDING ON`. O preenchimento é sempre ligado para **nchar**, mas para **char**, no caso em que as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.                                                                                                                                                                                                                                                                                                                                                                                      |
| Comprimento variável | Os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** e **nvarchar** são mapeados diretamente para os tipos **VARCHAR** e **NVARCHAR** do JDBC, respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| long            | Os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **text** e **ntext** são mapeados para os tipos **LONGVARCHAR** e **LONGNVARCHAR** do JDBC, respectivamente. Esses são tipos preteridos que começam com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]; portanto, você deve usar tipos de valor maiores, **varchar(max)** ou **nvarchar(max)** .<br /><br /> O uso dos métodos update\<Numeric Type> e [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) falhará com relação às colunas de servidor **text** e **ntext**. Porém, usar o método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) com um tipo de conversão de caractere especificado tem suporte para colunas de servidor de **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipos de cadeia de caracteres binária

Os tipos de cadeia de caracteres binária JDBC são **BINARY**, **VARBINARY** e **LONGVARBINARY**.  
  
| Type            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Comprimento fixo    | O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary** é mapeado diretamente para o tipo **BINARY** do JDBC. Esse é um tipo de comprimento fixo com preenchimento fornecido pelo servidor no caso em que a coluna possui SET ANSI_PADDING ON. Quando as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.<br /><br /> O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** é um tipo **BINARY** do JDBC com o comprimento fixo de 8 bytes. |
| Comprimento variável | O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** é mapeado para o tipo **VARBINARY** do JDBC.<br /><br /> O tipo **udt** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mapeado para JDBC como um tipo **VARBINARY**.                                                                                                                                                                                                                                 |
| long            | O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **image** é mapeado para o tipo **LONGVARBINARY** do JDBC. Esse tipo foi preterido desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], assim, você deve usar um tipo de valor grande, **varbinary(max)** no lugar dele.                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exatos

Os tipos numéricos exatos do JDBC mapeiam diretamente para os tipos do SQL Server correspondentes.  
  
| Type     | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | O tipo **BIT** do JDBC representa um único bit que pode ser 0 ou 1. Isso é mapeado para um tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit**.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | O tipo **TINYINT** do JDBC representa um único byte. Isso é mapeado para um tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint**.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | O tipo **SMALLINT** do JDBC representa um inteiro de 16 bits com sinal. Isso é mapeado para um tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint**.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | O tipo **INTEGER** do JDBC representa um inteiro de 32 bits com sinal. Isso é mapeado para um tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | O tipo **BIGINT** do JDBC representa um inteiro de 64 bits com sinal. Isso é mapeado para um tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint**.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | O tipo **NUMERIC** do JDBC representa um valor decimal de precisão fixa que contém valores de precisão idêntica. O tipo **NUMERIC** é mapeado para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numeric**.                                                                                                                                                                                                                                                                   |
| DECIMAL  | O tipo **DECIMAL** do JDBC representa um valor decimal de precisão fixa que contém valores pelo menos da precisão especificada. O tipo **DECIMAL** é mapeado para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal**.<br /><br /> O tipo **DECIMAL** do JDBC também é mapeado para os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **money** e **smallmoney**, que são tipos decimais de precisão fixa específicos armazenados em 8 e 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Os tipos numéricos aproximados do JDBC são **REAL**, **DOUBLE** e **FLOAT**.  
  
| Type   | Descrição                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | O tipo **REAL** do JDBC tem sete dígitos de precisão (precisão única) e é mapeado diretamente para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | O tipo **DOUBLE** do JDBC tem 15 dígitos de precisão (precisão dupla) e é mapeado para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**. O tipo **FLOAT** do JDBC é um sinônimo de **DOUBLE**. Como pode haver confusão entre **FLOAT** e **DOUBLE**, a preferência é **DOUBLE**. |
  
## <a name="datetime-types"></a>Tipos de Data e Hora

O tipo **TIMESTAMP** do JDBC é mapeado para os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** e **smalldatetime**. O tipo **datetime** é armazenado em dois inteiros de 4 bytes. O tipo **smalldatetime** contém as mesmas informações (data e hora), mas com menos exatidão, em dois inteiros pequenos de 2 bytes.  
  
> [!NOTE]  
> O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** é um tipo de cadeia de caracteres binária de comprimento fixo. Ele não é mapeado para nenhum dos tipos de hora do JDBC: **DATE**, **TIME** ou **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Mapeamento de tipo personalizado

O recurso de mapeamento de tipo personalizado do JDBC que usa as interfaces do SQLData para os tipos avançados do JDBC (UDTs, Struct e assim por diante). não é implementado no JDBC Driver.  
  
## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
