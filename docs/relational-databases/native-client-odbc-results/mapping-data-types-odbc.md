---
title: Mapeando tipos de dados (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd3bada9ea15d1104edb33024c4ab1476843c73b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779126"
---
# <a name="mapping-data-types-odbc"></a>Mapeando tipos de dados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mapeia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados SQL para tipos de dados SQL ODBC. As seções a seguir abordam os tipos de dados SQL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tipos de dados SQL ODBC para os quais é feito o mapeamento. Também são abordados os tipos de dados SQL ODBC e seus tipos de dados C ODBC correspondentes, além das conversões padrão e as com suporte.  
  
> [!NOTE]  
>  O tipo de dados **timestamp** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é mapeado para o tipo de dados SQL_BINARY ou SQL_VARBINARY ODBC porque os valores nas colunas **timestamp** não são valores **DateTime** , mas valores **binários (8)** ou **varbinary (8)** que indicam o sequência de atividade de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na linha. Se o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encontrar um valor SQL_C_WCHAR (Unicode) que tenha um número ímpar de bytes, o byte ímpar à direita será truncado.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>Lidando com o tipo de dados sql_variant no ODBC  
 A coluna de tipo de dados **sql_variant** pode conter qualquer um dos tipos de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto em objetos grandes (LOBs), como **Text**, **ntext**e **Image**. Por exemplo, a coluna pode conter valores **smallint** para algumas linhas, valores **flutuantes** para outras linhas e valores **Char/nchar** no restante.  
  
 O tipo de dados **sql_variant** é semelhante ao tipo de dados **variant** no Microsoft Visual Basic®.  
  
### <a name="retrieving-data-from-the-server"></a>Recuperando dados do servidor  
 O ODBC não tem um conceito de tipos variantes, limitando o uso do tipo de dados **sql_variant** com um driver ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se a associação for especificada, o tipo de dados **sql_variant** deverá ser associado a um dos tipos de dados ODBC documentados. **SQL_CA_SS_VARIANT_TYPE**, um novo atributo específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client, retorna o tipo de dados de uma instância na coluna **sql_variant** para o usuário.  
  
 Se nenhuma associação for especificada, a função [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) poderá ser usada para determinar o tipo de dados de uma instância na coluna **sql_variant** .  
  
 Para recuperar **sql_variant** dados, siga estas etapas.  
  
1.  Chame **SQLFetch** para posicionar para a linha recuperada.  
  
2.  Chame **SQLGetData**, especificando SQL_C_BINARY para o tipo e 0 para o comprimento dos dados. Isso força o driver a ler o cabeçalho de **sql_variant** . O cabeçalho fornece o tipo de dados dessa instância na coluna **sql_variant** . **SQLGetData** retorna o tamanho (em bytes) do valor.  
  
3.  Chame [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) especificando **SQL_CA_SS_VARIANT_TYPE** como seu valor de atributo. Essa função retornará o tipo de dados C da instância na coluna **sql_variant** para o cliente.  
  
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
  
 Se o usuário criar a Associação usando [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), o driver lerá os metadados e os dados. O driver converte os dados no tipo ODBC apropriado especificado na associação.  
  
### <a name="sending-data-to-the-server"></a>Enviando dados ao servidor  
 **SQL_SS_VARIANT**, um novo tipo de dados específico para o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, é usado para os dados enviados a uma coluna **sql_variant** . Ao enviar dados para o servidor usando parâmetros (por exemplo, inserir em valores de TableName (?,?)), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) é usado para especificar as informações de parâmetro, incluindo o tipo C e o tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client converterá o tipo de dados C em um dos subtipos de **sql_variant** apropriados.  
  
## <a name="see-also"></a>Consulte também  
 [Processando &#40;resultados ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
