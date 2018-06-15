---
title: Diferenças de tipo de dados de Conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5395b915d2f261813495d364730d0442a8139334
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853311"
---
# <a name="understanding-data-type-differences"></a>Entendendo diferenças de tipo de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Há algumas diferenças entre os tipos de dados de idioma programação Java e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ajuda a facilitar essas diferenças através de vários tipos de conversões.  
  
## <a name="character-types"></a>Tipos de caractere  
 Os tipos de dados de cadeia de caracteres do JDBC são **CHAR**, **VARCHAR**, e **LONGVARCHAR**. O driver JDBC oferece suporte à API do JDBC 4.0. No JDBC 4.0, os tipos de dados de cadeia de caracteres do JDBC também podem ser **NCHAR**, **NVARCHAR**, e **LONGNVARCHAR**. Estes novos tipos de cadeia de caracteres mantêm tipos de caracteres nativos de Java em formato Unicode e remove a necessidade de executar alguma conversão ANSI-para-Unicode ou Unicode-para-ANSI.  
  
|Tipo|Description|  
|----------|-----------------|  
|Comprimento fixo|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **char** e **nchar** tipos de dados são mapeados diretamente para o JDBC **CHAR** e **NCHAR** tipos. Estes são tipos de comprimentos fixos com preenchimento fornecidos pelo servidor no caso em que a coluna possui SET ANSI_PADDING ON. O preenchimento é sempre ligado para **nchar**, mas para **char**, no caso em que as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.|  
|Comprimento variável|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varchar** e **nvarchar** tipos são mapeados diretamente para o JDBC **VARCHAR** e **NVARCHAR** tipos, respectivamente.|  
|Longo|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **texto** e **ntext** tipos são mapeados para o JDBC **LONGVARCHAR** e **LONGNVARCHAR** digitar, respectivamente. Estes são tipos preteridos a partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], portanto, você deve usar tipos de valor grande, **varchar (max)** ou **nvarchar (max)**, em vez disso.<br /><br /> Usando a atualização\<tipo numérico > e [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) métodos falhará em **texto** e **ntext** colunas de servidor. No entanto, usando o [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) há suporte para o método com um tipo de conversão de caractere especificado em **texto** e **ntext** colunas de servidor.|  
  
## <a name="binary-string-types"></a>Tipos de cadeia de caracteres binária  
 Os tipos de cadeia de caracteres binários do JDBC são **binário**, **VARBINARY**, e **LONGVARBINARY**.  
  
|Tipo|Description|  
|----------|-----------------|  
|Comprimento fixo|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **binário** digite mapeia diretamente para o JDBC **binário** tipo. Esse é um tipo de comprimento fixo com preenchimento fornecido pelo servidor no caso em que a coluna possui SET ANSI_PADDING ON. Quando as colunas de char de servidor não são preenchidas, o driver JDBC adiciona o preenchimento.<br /><br /> O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **timestamp** tipo é um JDBC **binário** tipo com o comprimento fixo de 8 bytes.|  
|Comprimento variável|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varbinary** tipo é mapeado para o JDBC **VARBINARY** tipo.<br /><br /> O **udt** digite [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mapeia para o JDBC como um **VARBINARY** tipo.|  
|Longo|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **imagem** tipo é mapeado para o JDBC **LONGVARBINARY** tipo. Esse tipo foi substituído a partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], portanto, você deve usar um tipo de valor grande, **varbinary (max)** em vez disso.|  
  
## <a name="exact-numeric-types"></a>Tipos numéricos exatos  
 Os tipos numéricos exatos do JDBC mapeiam diretamente para os tipos do SQL Server correspondentes.  
  
|Tipo|Description|  
|----------|-----------------|  
|BIT|O JDBC **BIT** tipo representa um único bit que pode ser 0 ou 1. Isso mapeia para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bit** tipo.|  
|TINYINT|O JDBC **TINYINT** tipo representa um único byte. Isso mapeia para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tinyint** tipo.|  
|SMALLINT|O JDBC **SMALLINT** tipo representa um inteiro assinado de 16 bits. Isso mapeia para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **smallint** tipo.|  
|INTEGER|O JDBC **inteiro** tipo representa um inteiro assinado de 32 bits. Isso mapeia para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **int** tipo.|  
|bigint|O JDBC **BIGINT** tipo representa um inteiro assinado de 64 bits. Isso mapeia para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bigint** tipo.|  
|NUMERIC|O JDBC **NUMÉRICO** tipo representa um valor decimal de precisão fixa que contém os valores de precisão idêntica. O **NUMÉRICO** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **numérico** tipo.|  
|DECIMAL|O JDBC **DECIMAL** tipo representa um valor decimal de precisão fixa que contém os valores pelo menos a precisão especificada. O **DECIMAL** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **decimal** tipo.<br /><br /> O JDBC **DECIMAL** tipo também é mapeado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **money** e **smallmoney** tipos, que são específicos tipos de decimais de precisão fixa que são armazenados em 8 e 4 bytes, respectivamente.|  
  
## <a name="approximate-numeric-types"></a>Tipos numéricos aproximados  
 Os tipos numéricos aproximados do JDBC são **REAL**, **duplo**, e **FLOAT**.  
  
|Tipo|Description|  
|----------|-----------------|  
|REAL|O JDBC **REAL** tipo tem sete dígitos de precisão (precisão única) e mapeia diretamente para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **real** tipo.|  
|DOUBLE|O JDBC **duplo** tipo tem 15 dígitos de precisão (precisão dupla) e mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **float** tipo. O JDBC **FLOAT** tipo é um sinônimo do **duplo**. Como pode haver confusão entre **FLOAT** e **duplo**, **duplo** é preferencial.|  
  
## <a name="datetime-types"></a>Tipos de Data e Hora  
 O JDBC **TIMESTAMP** tipo mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** e **smalldatetime** tipos. O **datetime** tipo é armazenado em dois inteiros de 4 bytes. O **smalldatetime** tipo contém as mesmas informações (data e hora), mas com menos exatidão, em dois inteiros pequenos de 2 bytes.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **timestamp** é um tipo de cadeia de caracteres binária de comprimento fixo. Ele não mapeia para nenhum dos tipos de hora de JDBC: **data**, **tempo**, ou **TIMESTAMP**.  
  
## <a name="custom-type-mapping"></a>Mapeamento de tipo personalizado  
 O recurso de mapeamento de tipo personalizado do JDBC que usa as interfaces de dados Sqlz para o JDBC avançada tipos (UDTs, Struct e assim por diante). não é implementado no JDBC Driver.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
