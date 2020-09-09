---
description: sp_OAGetErrorInfo (Transact-SQL)
title: sp_OAGetErrorInfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 89bb7dff2131d8463e26754148aa6e8032503fd7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545992"
---
# <a name="sp_oageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Obtém informações sobre erro de Automação OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OAGetErrorInfo [ objecttoken ]  
    [ , source OUTPUT ]   
    [ , description OUTPUT ]   
    [ , helpfile OUTPUT ]   
    [ , helpid OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 É o token do objeto de um objeto OLE criado anteriormente usando **sp_OACreate** ou é nulo. Se *objecttoken* for especificado, as informações de erro para esse objeto serão retornadas. Se o NULL for especificado, serão retornadas as informações de erro para o lote inteiro.  
  
 _source_ **saída** de origem  
 É a origem das informações de erro. Se especificado, ele deve ser uma variável **Char**, **nchar**, **varchar**ou **nvarchar** local. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 _description_ **saída** da descrição  
 É a descrição do erro. Se especificado, ele deve ser uma variável **Char**, **nchar**, **varchar**ou **nvarchar** local. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 _helpfile_ **saída** de ArquivoDeAjuda  
 É o arquivo de ajuda para o objeto OLE. Se especificado, ele deve ser uma variável **Char**, **nchar**, **varchar**ou **nvarchar** local. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 **saída** da _HelpID_  
 É a ID de contexto do arquivo de ajuda. Se especificado, ele deve ser uma variável **int** local.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [códigos de retorno de automação OLE e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum parâmetro de saída for especificado, as informações de erro serão retornadas ao cliente como um conjunto de resultados.  
  
|Nomes de coluna|Tipo de dados|Descrição|  
|------------------|---------------|-----------------|  
|**Erro**|**Binary (4)**|Representação binária do número do erro.|  
|**Origem**|**nvarchar (nn)**|A origem do erro.|  
|**Descrição**|**nvarchar (nn)**|Descrição do erro.|  
|**HelpFile**|**nvarchar (nn)**|Arquivo de ajuda para a origem.|  
|**HelpID**|**int**|ID de contexto de ajuda do arquivo de origem da Ajuda.|  
  
## <a name="remarks"></a>Comentários  
 Cada chamada para um procedimento armazenado de automação OLE (exceto **sp_OAGetErrorInfo**) redefine as informações de erro; Portanto, **sp_OAGetErrorInfo** Obtém informações de erro apenas para a chamada de procedimento armazenado de automação OLE mais recente. Observe que, como **sp_OAGetErrorInfo** não redefine as informações de erro, ele pode ser chamado várias vezes para obter as mesmas informações de erro.  
  
 A tabela a seguir lista os erros de Automação OLE e suas causas comuns.  
  
|Erro e HRESULT|Causa comum|  
|-----------------------|------------------|  
|**Tipo de variável incorreto (0x80020008)**|O tipo de dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] valor passado como um parâmetro de método não correspondeu ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] tipo de dados do parâmetro Method ou um valor nulo foi passado como um parâmetro de método.|  
|**Nome desconhecido (0x8002006)**|A propriedade ou o nome de método especificado não foi localizado para o objeto especificado.|  
|**Cadeia de caracteres de classe inválida (0x800401f3)**|ProgID ou CLSID especificado não foi registrado como um objeto OLE em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os servidores de automação OLE personalizados devem ser registrados antes de poderem ser instanciados usando **sp_OACreate**. Isso pode ser feito usando o utilitário de Regsvr32.exe para servidores em processo (. dll) ou a opção de linha de comando **/RegServer** para servidores locais (. exe).|  
|**Execução do servidor falhou (0x80080005)**|O objeto OLE especificado foi registrado como um servidor OLE local (arquivo .exe), mas o arquivo .exe não pôde ser localizado ou iniciado.|  
|**O módulo especificado não pôde ser localizado (0x8007007e)**|O objeto OLE especificado foi registrado como um servidor OLE em processo (arquivo .dll), mas o arquivo .dll não pôde ser localizado ou carregado.|  
|**Incompatibilidade de tipos (0x80020005)**|O tipo de dados de uma variável local [!INCLUDE[tsql](../../includes/tsql-md.md)] usado para armazenar um valor de propriedade retornado ou um valor de retorno do método não correspondeu ao tipo de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] do valor de retorno da propriedade ou do método. Ou, o valor de retorno de uma propriedade ou de um método foi solicitado, mas não é retornado.|  
|**DataType ou Value do parâmetro ' Context ' de sp_OACreate é inválido. (0x8004275B)**|O valor do parâmetro de contexto deveria ser: 1, 4 ou 5.|  
  
 Para obter mais informações sobre o processamento de códigos de retorno HRESULT, consulte [códigos de retorno de automação OLE e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** ou a permissão execute diretamente neste procedimento armazenado. `Ole Automation Procedures` a configuração deve ser **habilitada** para usar qualquer procedimento do sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe informações sobre erro de Automação OLE.  
  
```  
DECLARE @output varchar(255);  
DECLARE @hr int;  
DECLARE @source varchar(255);  
DECLARE @description varchar(255);  
PRINT 'OLE Automation Error Information';  
EXEC @hr = sp_OAGetErrorInfo @object, @source OUT, @description OUT;  
IF @hr = 0  
BEGIN  
    SELECT @output = '  Source: ' + @source  
    PRINT @output  
    SELECT @output = '  Description: ' + @description  
    PRINT @output  
END  
ELSE  
BEGIN  
    PRINT '  sp_OAGetErrorInfo failed.'  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
