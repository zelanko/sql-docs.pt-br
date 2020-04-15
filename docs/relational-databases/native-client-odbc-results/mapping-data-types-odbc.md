---
title: Mapeamento de Tipos de Dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 92426c854758d07a9d62ec57510d202b870dd9f2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304612"
---
# <a name="mapping-data-types-odbc"></a>Mapeando tipos de dados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver Cliente Nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC mapeia os tipos de dados SQL para os tipos de dados SQL do ODBC. As seções a seguir abordam os tipos de dados SQL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tipos de dados SQL ODBC para os quais é feito o mapeamento. Também são abordados os tipos de dados SQL ODBC e seus tipos de dados C ODBC correspondentes, além das conversões padrão e as com suporte.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo **de datatipo de carimbo de data e hora** mapeia para o SQL_BINARY ou SQL_VARBINARY tipo de dados ODBC porque os valores nas colunas de carimbo de **data** não são valores **de data-hora,** mas **valores binários(8)** ou **varbinary(8)** que indicam a seqüência de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atividade na linha. Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um valor SQL_C_WCHAR (Unicode) que tenha um número ímpar de bytes, o byte ímpar à direita será truncado.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>Lidando com o tipo de dados sql_variant no ODBC  
 A **coluna sql_variant** tipo de dados pode [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conter qualquer um dos tipos de dados em, exceto objetos grandes (LOBs), como **texto,** **ntext**e **imagem**. Por exemplo, a coluna pode conter valores **pequenos** para algumas linhas, valores **flutuantes** para outras linhas e valores **de char/nchar** no restante.  
  
 O **sql_variant** tipo de dados é semelhante ao tipo de dados **variante** no Microsoft Visual Basic®.  
  
### <a name="retrieving-data-from-the-server"></a>Recuperando dados do servidor  
 A ODBC não possui um conceito de tipos **sql_variant** de variantes, limitando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]uso do sql_variant tipo de dados com um driver ODBC em . Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se a vinculação for especificada, **o** sql_variant tipo de dados deve ser vinculado a um dos tipos de dados ODBC documentados. **SQL_CA_SS_VARIANT_TYPE**, um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atributo específico para o driver Cliente Nativo ODBC, retorna o tipo de dados de uma instância na coluna **sql_variant** ao usuário.  
  
 Se nenhuma vinculação for especificada, a função [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) pode ser usada para determinar o tipo de dados de uma instância na coluna **sql_variant.**  
  
 Para recuperar **dados sql_variant** siga estas etapas.  
  
1.  Ligue para **o SQLFetch** para posicionar a linha recuperada.  
  
2.  Ligue para **sqlgetdata**, especificando SQL_C_BINARY para o tipo e 0 para o comprimento dos dados. Isso força o motorista a ler o **cabeçalho sql_variant.** O cabeçalho fornece o tipo de dados dessa instância na coluna **sql_variant.** **SQLGetData** retorna o tamanho (em bytes) do valor.  
  
3.  Ligue para [sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) especificando **SQL_CA_SS_VARIANT_TYPE** como seu valor de atributo. Esta função retornará o tipo de dados C da instância na coluna **sql_variant** ao cliente.  
  
 Aqui está um segmento de código que ilustra as etapas acima.  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 Se o usuário criar a vinculação usando [o SQLBindCol,](../../relational-databases/native-client-odbc-api/sqlbindcol.md)o driver lerá os metadados e os dados. O driver converte os dados no tipo ODBC apropriado especificado na associação.  
  
### <a name="sending-data-to-the-server"></a>Enviando dados ao servidor  
 **SQL_SS_VARIANT**, um novo tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados específico do driver Cliente Nativo ODBC, é usado para dados enviados para uma coluna **de sql_variant.** Ao enviar dados para o servidor usando parâmetros (por exemplo, INSERT INTO TableName VALUES (?,?)), [o SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) é usado para especificar as informações do parâmetro, incluindo o tipo C e o tipo correspondente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Cliente Nativo converterá o tipo de dados C em um dos subtipos **sql_variant** apropriados.  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados de processamento &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
