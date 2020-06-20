---
title: IBCPSession::BCPInit (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IBCPSession::BCPInit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- BCPInit method
ms.assetid: 583096d7-da34-49be-87fd-31210aac81aa
author: rothja
ms.author: jroth
ms.openlocfilehash: 3709b32e8db1027bce963f22b6fe282e120ad4f4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048010"
---
# <a name="ibcpsessionbcpinit-ole-db"></a>IBCPSession::BCPInit (OLE DB)
  Inicializa a estrutura de cópia em massa, executa alguma verificação de erros, verifica se os nomes dos arquivos de formato e de dados estão corretos e, então, os abre.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPInit(   
const wchar_t *pwszTable,  
const wchar_t *pwszDataFile,  
const wchar_t *pwszErrorFile,  
inteDirection);  
```  
  
## <a name="remarks"></a>Comentários  
 O método **BCPInit** deve ser chamado antes de qualquer outro método de cópia em massa. O método **BCPInit** executa as inicializações necessárias para uma cópia em massa de dados entre a estação de trabalho e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O método **BCPInit** examina a estrutura da tabela de origem ou de destino do banco de dados, não o arquivo de dados. Ele especifica valores de formato de dados para o arquivo de dados com base em cada coluna na tabela, exibição ou conjunto de resultados SELECT do banco de dados. Essa especificação inclui o tipo de dados de cada coluna, a presença ou ausência de um indicador de comprimento ou nulo e cadeias de caracteres de bytes de terminador nos dados, além da largura de tipos de dados de comprimento fixo. O método **BCPInit** define esses valores da seguinte maneira:  
  
-   O tipo de dados especificado é o tipo de dados da coluna na tabela, exibição ou conjunto de resultados de SELECT do banco de dados. O tipo de dados é enumerado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados nativos especificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivo de cabeçalho nativo do cliente (sqlncli. h). Seus valores estão no padrão de BCP_TYPE_XXX. Os dados são representados em seu formato de computador. Ou seja, os dados de uma coluna com o tipo de dados inteiro são representados por uma sequência de quatro bytes baseado em big ou little endian no computador que criou o arquivo de dados.  
  
-   Se um tipo de dados de banco de dados tiver comprimento fixo, os dados do arquivo de dados também terão comprimento fixo. Os métodos de cópia em massa que processam dados (por exemplo, [IBCPSession::BCPExec](ibcpsession-bcpexec-ole-db.md)) analisam as linhas de dados esperando que o tamanho dos dados no arquivo de dados seja idêntico ao tamanho dos dados especificados na tabela, na exibição ou na lista de colunas SELECT do banco de dados. Por exemplo, os dados de uma coluna de banco de dados definida como `char(13)` devem ser representados por 13 caracteres para cada linha de dados no arquivo. Os dados de comprimento fixo podem ser prefixados com um indicador nulo se a coluna do banco de dados permitir valores nulos.  
  
-   Ao copiar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo de dados deve ter dados em cada coluna na tabela do banco de dados. Ao copiar dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados de todas as colunas na tabela, exibição ou conjunto de resultados de SELECT do banco de dados são copiados para o arquivo de dados.  
  
-   Ao copiar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a posição ordinal de uma coluna no arquivo de dados deve ser idêntica à posição ordinal da coluna na tabela do banco de dados. Ao copiar dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o método **BCPExec** coloca os dados com base na posição ordinal da coluna na tabela de banco de dados.  
  
-   Se um tipo de dados do banco de dados tiver comprimento variável (por exemplo, `varbinary(22)`) ou se uma coluna do banco de dados puder conter valores nulos, os dados nos arquivos de dados serão prefixados com um indicador de comprimento/nulo. A largura do indicador varia dependendo do tipo de dados e da versão da cópia em massa. A opção BCP_OPTION_FILEFMT do método [IBCPSession::BCPControl](ibcpsession-bcpcontrol-ole-db.md) oferece compatibilidade entre arquivos de dados de cópia em massa anteriores e servidores que executam versões posteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indicando quando a largura dos indicadores nos dados é mais estreita que o esperado.  
  
> [!NOTE]  
>  Para alterar os valores de formato de dados especificados para um arquivo de dados, use os métodos [IBCPSession::BCPColumns](ibcpsession-bcpcolumns-ole-db.md) e [IBCPSession::BCPColFmt](ibcpsession-bcpcolfmt-ole-db.md).  
  
 É possível otimizar cópias em massa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tabelas que não contêm índices, definindo a opção de banco de dados **select into/bulkcopy**.  
  
## <a name="arguments"></a>Argumentos  
 *pwszTable*[in]  
 O nome da tabela do banco de dados a ser copiada de ou para. O nome pode incluir o nome do banco de dados ou o nome do proprietário. Por exemplo, "pubs.username.titles", "pubs..titles", "username.titles".  
  
 Se o argumento eDirection for definido como BCP_DIRECTION_OUT, o argumento pwszTable poderá ser o nome de uma exibição do banco de dados.  
  
 Se o argumento eDirection for definido como BCP_DIRECTION_OUT e uma instrução SELECT for especificada usando o método **BCPControl** antes de o método **BCPExec** ser chamado, o argumento *pwszTable* precisará ser definido como NULL.  
  
 *pwszDataFile*[in]  
 O nome do arquivo do usuário a ser copiado de ou para.  
  
 *pwszErrorFile*[in]  
 O nome do arquivo de erro a ser preenchido com mensagens de progresso, mensagens de erro e cópias das linhas que não puderam ser copiadas de um arquivo do usuário para uma tabela. Se o argumento *pwszErrorFile* for definido como NULL, nenhum arquivo de erro será usado.  
  
 *eDirection*[in]  
 A direção da operação de cópia, BCP_DIRECTION_IN ou _OUT de BCP_DIRECTION. BCP_DIRECTION _IN indica uma cópia de um arquivo do usuário para uma tabela do banco de dados; BCP_DIRECTION _OUT indica uma cópia de uma tabela do banco de dados para um arquivo do usuário.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_FAIL  
 Ocorreu um erro específico do provedor ' para obter informações detalhadas, use a interface [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) .  
  
 E_OUTOFMEMORY  
 Erro de memória insuficiente.  
  
 E_INVALIDARG  
 Um ou mais dos argumentos não foi especificado corretamente. Por exemplo, foi especificado um nome de arquivo inválido.  
  
## <a name="see-also"></a>Consulte Também  
 [IBCPSession &#40;OLE DB&#41;](ibcpsession-ole-db.md)   
 [Executando operações de cópia em massa](../native-client/features/performing-bulk-copy-operations.md)  
  
  
