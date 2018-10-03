---
title: Diferenças de tipo de dados de Conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 546dc71fad06fc69d816d16c1d6c2d67f59f968b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773196"
---
# <a name="understanding-data-type-differences"></a>Entendendo diferenças de tipo de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Há várias diferenças entre os tipos de dados da linguagem de programação Java e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ajuda a facilitar essas diferenças por meio de vários tipos de conversões.  

## <a name="character-types"></a>Tipos de caractere

Os tipos de dados de cadeia de caracteres do JDBC são **CHAR**, **VARCHAR**, e **LONGVARCHAR**. O driver JDBC oferece suporte à API do JDBC 4.0. No JDBC 4.0, os tipos de dados de cadeia de caracteres do JDBC também podem ser **NCHAR**, **NVARCHAR**, e **LONGNVARCHAR**. Estes novos tipos de cadeia de caracteres mantêm tipos de caracteres nativos de Java em formato Unicode e remove a necessidade de executar alguma conversão ANSI-para-Unicode ou Unicode-para-ANSI.  
  
| Tipo            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Comprimento fixo    | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char** e **nchar** tipos de dados são mapeados diretamente para o JDBC **CHAR** e **NCHAR** tipos. São tipos de comprimentos fixos com preenchimento fornecidos pelo servidor caso a coluna tenha `SET ANSI_PADDING ON`. O preenchimento é sempre ligado para **nchar**, mas para **char**, no caso em que as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.                                                                                                                                                                                                                                                                                                                                                                                      |
| Comprimento variável | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar** e **nvarchar** tipos são mapeados diretamente para o JDBC **VARCHAR** e **NVARCHAR** tipos, respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Longo            | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto** e **ntext** tipos são mapeados para o JDBC **LONGVARCHAR** e **LONGNVARCHAR** digitar, respectivamente. Estes são tipos substituídos a partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], portanto, você deve usar tipos de valor grande **varchar (max)** ou **nvarchar (max)**, em vez disso.<br /><br /> Usando a atualização\<tipo numérico > e [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) métodos não funcionará em **texto** e **ntext** colunas de servidor. Porém, usar o método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) com um tipo de conversão de caractere especificado tem suporte para colunas de servidor de **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipos de cadeia de caracteres binária

Os tipos de cadeia de caracteres binários do JDBC são **binário**, **VARBINARY**, e **LONGVARBINARY**.  
  
| Tipo            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Comprimento fixo    | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binário** tipo é mapeado diretamente para o JDBC **binário** tipo. Esse é um tipo de comprimento fixo com preenchimento fornecido pelo servidor no caso em que a coluna possui SET ANSI_PADDING ON. Quando as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** o tipo é um JDBC **binário** tipo com o comprimento fixo de 8 bytes. |
| Comprimento variável | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varbinary** tipo é mapeado para o JDBC **VARBINARY** tipo.<br /><br /> O **udt** digitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeia para o JDBC como um **VARBINARY** tipo.                                                                                                                                                                                                                                 |
| Longo            | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **imagem** tipo é mapeado para o JDBC **LONGVARBINARY** tipo. Esse tipo foi preterido desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], assim, você deve usar um tipo de valor grande, **varbinary(max)** no lugar dele.                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exatos

Os tipos numéricos exatos do JDBC mapeiam diretamente para os tipos do SQL Server correspondentes.  
  
| Tipo     | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | O tipo **BIT** do JDBC representa um único bit que pode ser 0 ou 1. Isso é mapeado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** tipo.                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | O tipo **TINYINT** do JDBC representa um único byte. Isso é mapeado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint** tipo.                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | O tipo **SMALLINT** do JDBC representa um inteiro de 16 bits com sinal. Isso é mapeado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint** tipo.                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | O tipo **INTEGER** do JDBC representa um inteiro de 32 bits com sinal. Isso é mapeado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int** tipo.                                                                                                                                                                                                                                                                                                                                           |
| bigint   | O tipo **BIGINT** do JDBC representa um inteiro de 64 bits com sinal. Isso é mapeado para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint** tipo.                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | O tipo **NUMERIC** do JDBC representa um valor decimal de precisão fixa que contém valores de precisão idêntica. O **numéricos** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **numérico** tipo.                                                                                                                                                                                                                                                                   |
| DECIMAL  | O tipo **DECIMAL** do JDBC representa um valor decimal de precisão fixa que contém valores pelo menos da precisão especificada. O **decimais** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal** tipo.<br /><br /> O tipo **DECIMAL** do JDBC também é mapeado para os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** e **smallmoney**, que são tipos decimais de precisão fixa específicos armazenados em 8 e 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Os tipos numéricos aproximados do JDBC são **reais**, **duplo**, e **FLOAT**.  
  
| Tipo   | Descrição                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | O tipo **REAL** do JDBC tem sete dígitos de precisão (precisão única) e mapeia diretamente para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | O tipo **DOUBLE** do JDBC tem 15 dígitos de precisão (precisão dupla) e é mapeado para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**float**. O JDBC **FLUTUAR** tipo é um sinônimo de **duplo**. Como pode haver confusão entre **FLUTUAR** e **duplo**, **DOUBLE** é preferencial. |
  
## <a name="datetime-types"></a>Tipos de Data e Hora

O JDBC **TIMESTAMP** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** e **smalldatetime** tipos. O tipo **datetime** é armazenado em dois inteiros de 4 bytes. O tipo **smalldatetime** contém as mesmas informações (data e hora), mas com menos exatidão, em dois inteiros pequenos de 2 bytes.  
  
> [!NOTE]  
> O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**timestamp** tem cadeia de caracteres binária de comprimento fixo. Ele não mapeia para qualquer um dos tipos de hora de JDBC: **data**, **tempo**, ou **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Mapeamento de tipo personalizado

O recurso de mapeamento de tipo personalizado do JDBC que usa as interfaces do SQLData para os tipos avançados do JDBC (UDTs, Struct e assim por diante). não é implementado no JDBC Driver.  
  
## <a name="see-also"></a>Consulte Também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
