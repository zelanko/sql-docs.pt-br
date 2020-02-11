---
title: bcp_control | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_control
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_control function
ms.assetid: 32187282-1385-4c52-9134-09f061eb44f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 323ea04d32501f04156ffa81452fad5e5cf86664
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62689526"
---
# <a name="bcp_control"></a>bcp_control
  Altera as configurações padrão de vários parâmetros de controle para uma cópia em massa entre um arquivo e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_control (  
HDBC   
hdbc  
,  
INT   
eOption  
,  
void*   
iValue  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *eOption*  
 É um dos seguintes:  
  
 BCPABORT  
 Para uma operação de cópia em massa que já está em andamento. Chame **bcp_control** com um *eOption* de BCPABORT de outro thread para interromper uma operação de cópia em massa em execução. O parâmetro *iValue* é ignorado.  
  
 BCPBATCH  
 É o número de linhas por lote. O padrão é 0, que indica todas as linhas de uma tabela, quando os dados estão sendo extraídos, ou todas as linhas no arquivo de dados do usuário, quando os dados estão sendo copiados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um valor menor que 1 redefine BCPBATCH para o padrão.  
  
 BCPDELAYREADFMT  
 Um booliano, se definido como true, fará com que [bcp_readfmt](bcp-readfmt.md) seja lido na execução. Se for false (o padrão), bcp_readfmt lerá imediatamente o arquivo de formato. Ocorrerá um erro de sequência se BCPDELAYREADFMT for true e você chamar bcp_columns ou bcp_setcolfmt.  
  
 Um erro de sequência também ocorrerá se você `bcp_control(hdbc,` chamar`, (void *)FALSE)` BCPDELAYREADFMT depois `bcp_control(hdbc,` de`, (void *)TRUE)` chamar BCPDELAYREADFMT e bcp_writefmt.  
  
 Para obter mais informações, veja [Descoberta de metadados](../native-client/features/metadata-discovery.md).  
  
 BCPFILECP  
 *iValue* contém o número da página de código para o arquivo de dados. Você pode especificar o número da página de código, como 1252 ou 850, ou como um destes valores:  
  
 BCPFILE_ACP: os dados no arquivo estão no Microsoft Windows?? página de código do cliente.  
  
 BCPFILE_OEMCP: os dados do arquivo estão na página de código OEM do cliente (padrão).  
  
 BCPFILE_RAW: os dados do arquivo estão na página de código do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 BCPFILEFMT  
 O número de versão do formato de arquivo de dados. Pode ser 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) ou 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). 120 é o padrão. Isso é útil para exportar e importar dados em formatos que tinham suporte em versões anteriores do servidor. Por exemplo, para importar dados que foram obtidos de uma coluna de texto em [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] um servidor em uma coluna **varchar (max)** em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] um servidor ou posterior, você deve especificar 80. Da mesma forma, se você especificar 80 ao exportar dados de uma coluna **varchar (max)** , ele será salvo da mesma forma que as [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] colunas de texto são salvas no formato e pode ser importado [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] para uma coluna de texto de um servidor.  
  
 BCPFIRST  
 É a primeira linha de dados a ser copiada em um arquivo ou tabela. O padrão é 1; um valor menor que 1 redefine essa opção para seu valor padrão.  
  
 BCPFIRSTEX  
 Para operações de saída BCP, especifica a primeira linha da tabela do banco de dados a ser copiada no arquivo de dados.  
  
 Para BCP em operações, especifica a primeira linha do arquivo de dados a ser copiada na tabela de banco de dados.  
  
 Espera-se que o parâmetro *iValue* seja o endereço de um inteiro de 64 bits assinado contendo o valor. O valor máximo que pode ser passado a BCPFIRSTEX é 2^63-1.  
  
 BCPFMTXML  
 Especifica que o arquivo de formato gerado deve estar no formato XML. Eles está desativado por padrão.  
  
 Os arquivos de formato XML apresentam maior flexibilidade, mas com alguns restrições adicionadas. Por exemplo, você não pode especificar o prefixo e o terminador para um campo simultaneamente, o que era possível nos arquivos de formato mais antigos.  
  
> [!NOTE]  
>  Os arquivos de formato XML só são suportados quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado junto com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 BCPHINTS  
 *iValue* contém um ponteiro de cadeia de caracteres SQLTCHAR. A cadeia de caracteres endereçada especifica dicas de processamento da cópia em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou uma instrução Transact-SQL que retorna um conjunto de resultados. Se uma instrução Transact-SQL especificada retornar mais de um conjunto de resultados, todos os conjuntos de resultados depois do primeiro serão ignorados. Para obter mais informações sobre dicas de processamento de cópia em massa, consulte [utilitário bcp](../../tools/bcp-utility.md).  
  
 BCPKEEPIDENTITY  
 Quando *iValue* é true, especifica que as funções de cópia em massa inserem valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados fornecidos para colunas definidas com uma restrição de identidade. O arquivo de entrada deve fornecer valores para as colunas de identidade. Se essa opção não for definida, novos valores de identidade serão gerados para as linhas inseridas. Quaisquer dados contidos no arquivo para as colunas de identidade serão ignorados.  
  
 BCPKEEPNULLS  
 Especifica se valores de dados vazios no arquivo serão convertidos em valores NULL na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando *iValue* for true, os valores vazios serão convertidos em NULL na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. O padrão será converter valores vazios em um valor padrão para a coluna na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se houver um padrão.  
  
 BCPLAST  
 É a última linha a ser copiada. O padrão é copiar todas as linhas; um valor menor que 1 redefine essa opção para seu padrão.  
  
 BCPLASTEX  
 Para operações de saída BCP, especifica a última linha da tabela do banco de dados a ser copiada no arquivo de dados.  
  
 Para BCP em operações, especifica a última linha do arquivo de dados a ser copiada na tabela do banco de dados.  
  
 Espera-se que o parâmetro *iValue* seja o endereço de um inteiro de 64 bits assinado contendo o valor. O valor de máximo que pode ser passado para BCPLASTEX é 2^63-1.  
  
 BCPMAXERRS  
 É o número de erros permitido antes de ocorrer uma falha na operação de cópia em massa. O padrão é 10; um valor menor que 1 redefine essa opção como seu padrão. A cópia em massa impõe um máximo de 65.535 erros. Uma tentativa de definir esta opção como um valor maior que 65.535 resulta na definição da opção como 65.535.  
  
 BCPODBC  
 Quando TRUE, especifica que os valores **DateTime** e **smalldatetime** salvos no formato de caractere usarão o prefixo e o sufixo da sequência de saída do carimbo de data e hora do ODBC. A opção BCPODBC só se aplica a BCP_OUT.  
  
 Quando for falso, um valor **DateTime** que representa 1º de janeiro de 1997 será convertido para a cadeia de caracteres: 1997-01-01 00:00:00.000. Quando TRUE, o mesmo valor **DateTime** é representado como: {ts ' 1997-01-01 00:00:00.000 '}.  
  
 BCPROWCOUNT  
 Retorna o número de linhas afetadas pela operação BCP atual (ou última).  
  
 BCPTEXTFILE  
 Quando TRUE, especifica que o arquivo de dados é um arquivo de texto, em vez de um arquivo binário. Se o arquivo for um arquivo de texto, BCP determinará se ele é ou não Unicode, verificando o marcador de bytes Unicode nos dois primeiros bytes do arquivo de dados.  
  
 BCPUNICODEFILE  
 Quando TRUE, especifica que o arquivo de entrada é um arquivo Unicode.  
  
 *iValue*  
 É o valor para o *eOption*especificado. *iValue* é uma conversão de valor inteiro (LONGLONG) em um ponteiro void para permitir a expansão futura para valores de 64 bits.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Esta função define vários parâmetros de controle para operações de cópia em massa, incluindo o número de erros permitido antes do cancelamento de uma cópia em massa, os número da primeira e da última linhas a serem copiadas de um arquivo de dados e o tamanho do lote.  
  
 Esta função é usada também para especificar a instrução SELECT durante uma operação de cópia em massa de saída do conjunto de resultados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma SELECT. Defina *eOption* como BCPHINTS e defina *iValue* para ter um ponteiro para uma cadeia de caracteres SQLTCHAR contendo a instrução SELECT.  
  
 Esses parâmetros de controle só são úteis ao fazer cópias entre um arquivo de usuário e uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As configurações de parâmetros de controle não têm nenhum efeito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre as linhas copiadas para com [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="example"></a>Exemplo  
  
```  
// Variables like henv not specified.  
SQLHDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("address"), _T("address.add"), _T("addr.err"),  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the number of rows per batch.   
if (bcp_control(hdbc, BCPBATCH, (void*) 1000) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set file column count.   
if (bcp_columns(hdbc, 1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the file format.   
if (bcp_colfmt(hdbc, 1, 0, 0, SQL_VARLEN_DATA, '\n', 1, 1)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
printf_s("%ld rows processed by bulk copy.", nRowsProcessed);  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
