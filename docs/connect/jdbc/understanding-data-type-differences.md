---
title: Entendendo diferenças de tipo de dados | Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027377"
---
# <a name="understanding-data-type-differences"></a>Entendendo diferenças de tipo de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Há várias diferenças entre os tipos de dados da linguagem de programação Java e os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ajuda a facilitar essas diferenças por meio de vários tipos de conversões.  

## <a name="character-types"></a>Tipos de caracteres

Os tipos de dados de cadeia de caracteres JDBC são **Char**, **varchar**e **LONGVARCHAR**. O driver JDBC oferece suporte à API do JDBC 4.0. No JDBC 4,0, os tipos de dados de cadeia de caracteres JDBC também podem ser **nchar**, **nvarchar**e **LONGNVARCHAR**. Estes novos tipos de cadeia de caracteres mantêm tipos de caracteres nativos de Java em formato Unicode e remove a necessidade de executar alguma conversão ANSI-para-Unicode ou Unicode-para-ANSI.  
  
| Tipo            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Comprimento fixo    | Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados **Char** e **nchar** são mapeados diretamente para os tipos JDBC **Char** e **nchar** . São tipos de comprimentos fixos com preenchimento fornecidos pelo servidor caso a coluna tenha `SET ANSI_PADDING ON`. O preenchimento é sempre ligado para **nchar**, mas para **char**, no caso em que as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.                                                                                                                                                                                                                                                                                                                                                                                      |
| Comprimento variável | Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos **varchar** e **nvarchar** mapeiam diretamente para os tipos JDBC **varchar** e **nvarchar** , respectivamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Longo            | Os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos **Text** e **ntext** são mapeados para o tipo JDBC **LONGVARCHAR** e **LONGNVARCHAR** , respectivamente. Esses são tipos preteridos começando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]no, portanto, você deve usar tipos de valor grande, **varchar (max)** ou **nvarchar (max)** , em vez disso.<br /><br /> Usar o tipo\<numérico de atualização > e os métodos UpdateObject [(int, Java. lang. Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) falhará nas colunas **Text** e **ntext** Server. Porém, usar o método [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) com um tipo de conversão de caractere especificado tem suporte para colunas de servidor de **text** e **ntext**. |
  
## <a name="binary-string-types"></a>Tipos de cadeia de caracteres binária

Os tipos de cadeia de caracteres binária JDBC são **Binary**, **varbinary**e **LONGVARBINARY**.  
  
| Tipo            | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Comprimento fixo    | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **Binary** é mapeado diretamente para o tipo **binário** JDBC. Esse é um tipo de comprimento fixo com preenchimento fornecido pelo servidor no caso em que a coluna possui SET ANSI_PADDING ON. Quando as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de **carimbo de data/hora** é um tipo **binário** JDBC com o comprimento fixo de 8 bytes. |
| Comprimento variável | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **varbinary** é mapeado para o tipo JDBC **varbinary** .<br /><br /> O tipo **UDT** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é mapeado para JDBC como um tipo **varbinary** .                                                                                                                                                                                                                                 |
| Longo            | O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de **imagem** é mapeado para o tipo de **LONGVARBINARY** JDBC. Esse tipo foi preterido desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], assim, você deve usar um tipo de valor grande, **varbinary(max)** no lugar dele.                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>Tipos numéricos exatos

Os tipos numéricos exatos do JDBC mapeiam diretamente para os tipos do SQL Server correspondentes.  
  
| Tipo     | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | O tipo **BIT** do JDBC representa um único bit que pode ser 0 ou 1. Isso é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo de **bit** .                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | O tipo **TINYINT** do JDBC representa um único byte. Isso é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo **tinyint** .                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | O tipo **SMALLINT** do JDBC representa um inteiro de 16 bits com sinal. Isso é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo **smallint** .                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | O tipo **INTEGER** do JDBC representa um inteiro de 32 bits com sinal. Isso é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo **int** .                                                                                                                                                                                                                                                                                                                                           |
| bigint   | O tipo **BIGINT** do JDBC representa um inteiro de 64 bits com sinal. Isso é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um tipo **bigint** .                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | O tipo **NUMERIC** do JDBC representa um valor decimal de precisão fixa que contém valores de precisão idêntica. O tipo **numérico** é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo **numérico** .                                                                                                                                                                                                                                                                   |
| DECIMAL  | O tipo **DECIMAL** do JDBC representa um valor decimal de precisão fixa que contém valores pelo menos da precisão especificada. O tipo **decimal** é mapeado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo **decimal** .<br /><br /> O tipo **DECIMAL** do JDBC também é mapeado para os tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**money** e **smallmoney**, que são tipos decimais de precisão fixa específicos armazenados em 8 e 4 bytes, respectivamente. |
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados

Os tipos numéricos aproximados do JDBC são **real**, **Double**e **float**.  
  
| Tipo   | Descrição                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | O tipo **REAL** do JDBC tem sete dígitos de precisão (precisão única) e mapeia diretamente para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real**.                                                                                                                                     |
| DOUBLE | O tipo **DOUBLE** do JDBC tem 15 dígitos de precisão (precisão dupla) e é mapeado para o tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**float**. O tipo **float** do JDBC é um sinônimo de **Double**. Como pode haver confusão entre **float** e **Double**, o **Double** é preferencial. |
  
## <a name="datetime-types"></a>Tipos de Data e Hora

O tipo de **carimbo de data/hora** JDBC é mapeado para os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos **DateTime** e **smalldatetime** . O tipo **datetime** é armazenado em dois inteiros de 4 bytes. O tipo **smalldatetime** contém as mesmas informações (data e hora), mas com menos exatidão, em dois inteiros pequenos de 2 bytes.  
  
> [!NOTE]  
> O tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**timestamp** tem cadeia de caracteres binária de comprimento fixo. Ele não é mapeado para nenhum dos tipos de tempo do JDBC: **Data**, **hora**ou **carimbo**de data/hora.  
  
## <a name="custom-type-mapping"></a>Mapeamento de tipo personalizado

O recurso de mapeamento de tipo personalizado do JDBC que usa as interfaces do SQLData para os tipos avançados do JDBC (UDTs, Struct e assim por diante). não é implementado no JDBC Driver.  
  
## <a name="see-also"></a>Confira também

[Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
