---
title: Mapeando tipos de dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a06aaa5e983f424f2017632c167bc662ed643190
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703677"
---
# <a name="mapping-data-types-odbc"></a>Mapeando tipos de dados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapas de driver ODBC Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados SQL para tipos de dados SQL ODBC. As seções a seguir abordam os tipos de dados SQL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tipos de dados SQL ODBC para os quais é feito o mapeamento. Também são abordados os tipos de dados SQL ODBC e seus tipos de dados C ODBC correspondentes, além das conversões padrão e as com suporte.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** tipo de dados mapeia para o tipo de dados SQL_BINARY ou SQL_VARBINARY ODBC porque os valores em **timestamp** colunas não estão **datetime** valores, mas **binary (8)** ou **varbinary (8)** valores que indicam a sequência de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atividade na linha. Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um valor SQL_C_WCHAR (Unicode) que tenha um número ímpar de bytes, o byte ímpar à direita será truncado.  
  
## <a name="dealing-with-sqlvariant-data-type-in-odbc"></a>Lidando com o tipo de dados sql_variant no ODBC  
 O **sql_variant** coluna de tipo de dados pode conter qualquer um dos tipos de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exceto LOBs (objetos grandes), como **texto**, **ntext**, e  **imagem**. Por exemplo, a coluna pode conter **smallint** valores para algumas linhas, **float** valores para as outras linhas, e **char/nchar** valores no restante.  
  
 O **sql_variant** tipo de dados é semelhante do **Variant** Microsoft Visual Basic® tipo de dados.  
  
### <a name="retrieving-data-from-the-server"></a>Recuperando dados do servidor  
 ODBC não têm um conceito de tipos variantes, limitando o uso do **sql_variant** tipo de dados com um driver ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se a associação é especificada, o **sql_variant** tipo de dados deve ser associado a um dos tipos de dados ODBC documentados. **SQL_CA_SS_VARIANT_TYPE**, um novo atributo específico para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC Native Client, retorna o tipo de dados de uma instância no **sql_variant** coluna para o usuário.  
  
 Se nenhuma associação for especificada, o [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) função pode ser usada para determinar o tipo de dados de uma instância no **sql_variant** coluna.  
  
 Para recuperar **sql_variant** dados siga estas etapas.  
  
1.  Chamar **SQLFetch** para posicionar na linha recuperada.  
  
2.  Chamar **SQLGetData**, especificando SQL_C_BINARY para o tipo e 0 para o comprimento de dados. Isso força o driver para ler o **sql_variant** cabeçalho. O cabeçalho fornece o tipo de dados da instância no **sql_variant** coluna. **SQLGetData** retorna o tamanho (em bytes) do valor.  
  
3.  Chamar [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) especificando **SQL_CA_SS_VARIANT_TYPE** como seu valor de atributo. Esta função retornará o tipo de dados C da instância de **sql_variant** coluna para o cliente.  
  
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
  
 Se o usuário cria a associação com [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), o driver lê os metadados e os dados. O driver converte os dados no tipo ODBC apropriado especificado na associação.  
  
### <a name="sending-data-to-the-server"></a>Enviando dados ao servidor  
 **SQL_SS_VARIANT**, um novo tipo de dados específico para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o driver ODBC Native Client, é usado para dados enviados para um **sql_variant** coluna. Ao enviar dados para o servidor usando parâmetros (por exemplo, INSERT INTO TableName VALUES (?,?)), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) é usado para especificar as informações de parâmetro, incluindo o tipo C e correspondente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client converterá o tipo de dados C em um dos **sql_variant** subtipos.  
  
## <a name="see-also"></a>Consulte também  
 [Processando resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
