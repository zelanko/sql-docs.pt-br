---
title: sp_OACreate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OACreate
- sp_OACreate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OACreate
ms.assetid: eb84c0f1-26dd-48f9-9368-13ee4a30a27c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 511101642570c9ddf28763b6303aa90bb985317a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752778"
---
# <a name="sp_oacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Cria uma instância de um objeto OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *progid*  
 É o identificador programático (ProgID) do objeto OLE a ser criado. Essa cadeia de caracteres descreve a classe do objeto OLE e tem o formato: **'**_OLEComponent_**.** _Objeto_**'**  
  
 *OLEComponent* é o nome do componente do servidor de automação OLE e *Object* é o nome do objeto OLE. O objeto OLE especificado deve ser válido e deve dar suporte à interface **IDispatch** .  
  
 Por exemplo, SQLDMO. SQLServer é o ProgID do objeto SQL-DMO **SqlServer** . O SQL-DMO tem um nome de componente do SQLDMO, o objeto **SqlServer** é válido e (como todos os objetos SQL-DMO) o objeto **SqlServer** dá suporte a **IDispatch**.  
  
 *clsid*  
 É o CLSID (identificador de classe) do objeto OLE a ser criado. Esta cadeia de caracteres descreve a classe do objeto OLE e tem o formato: **' {**_nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn_**} '**. O objeto OLE especificado deve ser válido e deve dar suporte à interface **IDispatch** .  
  
 Por exemplo, {00026BA1-0000-0000-C000-000000000046} é o CLSID do objeto SQL-DMO **SqlServer** .  
  
 **saída** de _objecttoken_  
 É o token do objeto retornado e deve ser uma variável local do tipo de dados **int**. Esse token de objeto identifica o objeto OLE criado e é usado em chamadas para os outros procedimentos armazenados de automação OLE.  
  
 *contexto*  
 Especifica o contexto de execução no qual o objeto OLE recém-criado é executado. Se especificado, esse valor deve ser um dos seguintes:  
  
 **1** = servidor OLE em processo (. dll) somente.  
  
 **4** = somente servidor local (. exe) OLE.  
  
 **5** = servidor OLE no processo e local permitidos  
  
 Se não for especificado, o valor padrão será **5**. Esse valor é passado como o parâmetro *dwClsContext* da chamada para **CoCreateInstance**.  
  
 Se um servidor OLE em processo for permitido (usando um valor de contexto de **1** ou **5** ou não especificar um valor de contexto), ele terá acesso à memória e a outros recursos pertencentes ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um servidor OLE em processo pode danificar a memória ou os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e causar resultados imprevisíveis, como uma violação de acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando você especifica um valor de contexto de **4**, um servidor OLE local não tem acesso a nenhum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recurso e não pode danificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memória ou recursos.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, e não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [códigos de retorno de automação OLE e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Comentários  
 Se os procedimentos de automação OLE estiverem habilitados, uma chamada para **sp_OACreate** iniciará o ambiente de execução compartilhada da automação OLE. Para obter mais informações sobre como habilitar a automação OLE, consulte [opção de configuração de servidor OLE Automation procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md).  
  
 O OLE objeto criado é destruído automaticamente no término do lote de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** ou a permissão execute diretamente neste procedimento armazenado. `Ole Automation Procedures`a configuração deve ser **habilitada** para usar qualquer procedimento do sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-progid"></a>a. Usando ProgID  
 O exemplo a seguir cria um objeto SQL-DMO **SqlServer** usando seu ProgID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate 'SQLDMO.SQLServer', @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
### <a name="b-using-clsid"></a>B. Usando CLSID  
 O exemplo a seguir cria um objeto SQL-DMO **SqlServer** usando seu CLSID.  
  
```  
DECLARE @object int;  
DECLARE @hr int;  
DECLARE @src varchar(255), @desc varchar(255);  
EXEC @hr = sp_OACreate '{00026BA1-0000-0000-C000-000000000046}',  
    @object OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object, @src OUT, @desc OUT   
   raiserror('Error Creating COM Component 0x%x, %s, %s',16,1, @hr, @src, @desc)  
    RETURN  
END;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Opção de configuração de servidor OLE Automation procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
