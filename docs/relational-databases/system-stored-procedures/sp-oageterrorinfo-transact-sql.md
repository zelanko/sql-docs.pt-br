---
title: sp_OAGetErrorInfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OAGetErrorInfo_TSQL
- sp_OAGetErrorInfo
dev_langs: TSQL
helpviewer_keywords: sp_OAGetErrorInfo
ms.assetid: ceecea08-456f-4819-85d9-ecc9647d7187
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b4477349f95fc286fce553f81e449162d8de511
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spoageterrorinfo-transact-sql"></a>sp_OAGetErrorInfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtém informações sobre erro de Automação OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 É o token de objeto de um objeto OLE que foi criado anteriormente usando **sp_OACreate** ou é nulo. Se *objecttoken* for especificado, serão retornadas informações de erro para esse objeto. Se o NULL for especificado, serão retornadas as informações de erro para o lote inteiro.  
  
 *origem* **saída**  
 É a origem das informações de erro. Se especificado, ele deve ser um local **char**, **nchar**, **varchar**, ou **nvarchar** variável. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 *Descrição* **saída**  
 É a descrição do erro. Se especificado, ele deve ser um local **char**, **nchar**, **varchar**, ou **nvarchar** variável. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 *arquivo de Ajuda* **saída**  
 É o arquivo de ajuda para o objeto OLE. Se especificado, ele deve ser um local **char**, **nchar**, **varchar**, ou **nvarchar** variável. O valor de retorno é truncado para se ajustar à variável local se necessário.  
  
 *helpid* **saída**  
 É a ID de contexto do arquivo de ajuda. Se especificado, ele deve ser um local **int** variável.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [OLE Automation códigos de retorno e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se nenhum parâmetro de saída for especificado, as informações de erro serão retornadas ao cliente como um conjunto de resultados.  
  
|Nomes de coluna|Tipo de dados|Description|  
|------------------|---------------|-----------------|  
|**Erro**|**binary (4)**|Representação binária do número do erro.|  
|**Origem**|**nvarchar(nn)**|A origem do erro.|  
|**Description**|**nvarchar(nn)**|Descrição do erro.|  
|**Arquivo de ajuda**|**nvarchar(nn)**|Arquivo de ajuda para a origem.|  
|**HelpID**|**int**|ID de contexto de ajuda do arquivo de origem da Ajuda.|  
  
## <a name="remarks"></a>Comentários  
 Procedimento armazenado de cada chamada para uma automação OLE (exceto **sp_OAGetErrorInfo**) redefine as informações de erro; portanto, **sp_OAGetErrorInfo** obtém informações de erro somente para o OLE mais recente Chamada de procedimento armazenados de automação. Observe que, como **sp_OAGetErrorInfo** não redefine as informações de erro, ele pode ser chamado várias vezes para obter as mesmas informações de erro.  
  
 A tabela a seguir lista os erros de Automação OLE e suas causas comuns.  
  
|Erro e HRESULT|Causa comum|  
|-----------------------|------------------|  
|**Tipo de variável incorreto (0x80020008)**|Tipo de dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] valor passado como um parâmetro de método não correspondeu a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] tipo de dados do parâmetro de método ou um valor NULL foi passado como um parâmetro de método.|  
|**Nome desconhecido (0x8002006)**|A propriedade ou o nome de método especificado não foi localizado para o objeto especificado.|  
|**Cadeia de caracteres de classe inválida (0x800401f3)**|ProgID ou CLSID especificado não foi registrado como um objeto OLE em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Servidores de automação OLE personalizados devem ser registrados antes de serem instanciados usando **sp_OACreate**. Isso pode ser feito usando o utilitário Regsvr32.exe para servidores em processo (. dll), ou o **/REGSERVER** opção de linha de comando para servidores de local (.exe).|  
|**Execução do servidor falhou (0x80080005)**|O objeto OLE especificado foi registrado como um servidor OLE local (arquivo .exe), mas o arquivo .exe não pôde ser localizado ou iniciado.|  
|**O módulo especificado não pôde ser localizado (0x8007007e)**|O objeto OLE especificado foi registrado como um servidor OLE em processo (arquivo .dll), mas o arquivo .dll não pôde ser localizado ou carregado.|  
|**Incompatibilidade de (tipos 0x80020005)**|O tipo de dados de uma variável local [!INCLUDE[tsql](../../includes/tsql-md.md)] usado para armazenar um valor de propriedade retornado ou um valor de retorno do método não correspondeu ao tipo de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] do valor de retorno da propriedade ou do método. Ou, o valor de retorno de uma propriedade ou de um método foi solicitado, mas não é retornado.|  
|**Tipo de dados ou valor do parâmetro 'context' de sp_OACreate é inválido (0x8004275B)**|O valor do parâmetro de contexto deveria ser: 1, 4 ou 5.|  
  
 Para obter mais informações sobre como processar códigos de retorno HRESULT, consulte [OLE Automation códigos de retorno e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Automação OLE armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
