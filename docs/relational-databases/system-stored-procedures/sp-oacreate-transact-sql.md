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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b7a56afb2ffa11dbe4ec8937efb602c13c9599d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65450022"
---
# <a name="spoacreate-transact-sql"></a>sp_OACreate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma instância de um objeto OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OACreate { progid | clsid } , objecttoken OUTPUT [ , context ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *progid*  
 É o identificador programático (ProgID) do objeto OLE a ser criado. Essa cadeia de caracteres descreve a classe do objeto OLE e tem o formato: **'** _OLEComponent_ **.** _Objeto_ **'**  
  
 *OLEComponent* é o nome do componente do servidor de automação OLE, e *objeto* é o nome do objeto OLE. O objeto OLE especificado deve ser válido e deve oferecer suporte a **IDispatch** interface.  
  
 Por exemplo, SQLDMO. SQL Server é o ProgID do SQL-DMO **SQLServer** objeto. SQL-DMO tem um nome de componente de SQLDMO, o **SQLServer** objeto é válido e (como o SQL-DMO todos os objetos) a **SQLServer** objeto dá suporte à **IDispatch**.  
  
 *clsid*  
 É o CLSID (identificador de classe) do objeto OLE a ser criado. Essa cadeia de caracteres descreve a classe do objeto OLE e tem o formato: **' {** _nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn_ **}'** . O objeto OLE especificado deve ser válido e deve oferecer suporte a **IDispatch** interface.  
  
 Por exemplo, {00026ba1-0000-0000-C000-000000000046} é o CLSID do SQL-DMO **SQLServer** objeto.  
  
 _objecttoken_ **OUTPUT**  
 É o token de objeto retornado, e deve ser uma variável local de tipo de dados **int**. Esse token de objeto identifica o objeto OLE criado e é usado em chamadas para os outros procedimentos armazenados de automação OLE.  
  
 *context*  
 Especifica o contexto de execução no qual o objeto OLE recém-criado é executado. Se especificado, esse valor deve ser um dos seguintes:  
  
 **1** = somente no servidor OLE em processo (. dll).  
  
 **4** = local (.exe) OLE somente do servidor.  
  
 **5** = server OLE em processo e local permitido  
  
 Se não for especificado, o valor padrão é **5**. Esse valor é passado como o *dwClsContext* parâmetro da chamada para **CoCreateInstance**.  
  
 Se um servidor OLE em processo é permitido (usando o valor de contexto de **1** ou **5** ou não especificando um valor de contexto), ele tem acesso à memória e outros recursos pertencentes ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um servidor OLE em processo pode danificar a memória ou os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e causar resultados imprevisíveis, como uma violação de acesso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando você especifica um valor de contexto de **4**, um servidor OLE local não tem acesso a qualquer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos e ele não podem danificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memória ou recursos.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, e não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [OLE automação códigos de retorno e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Comentários  
 Se procedimentos de automação OLE forem habilitados, uma chamada para **sp_OACreate** iniciará o ambiente de execução compartilhado de automação OLE. Para obter mais informações sobre como habilitar a automação OLE, consulte [Ole automação procedimentos Server Configuration Option](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md).  
  
 O OLE objeto criado é destruído automaticamente no término do lote de instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **sysadmin** função de servidor fixa ou permissão de execução diretamente nesse procedimento armazenado. `Ole Automation Procedures` configuração deve estar **habilitado** usar qualquer procedimento de sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-progid"></a>A. Usando ProgID  
 O exemplo a seguir cria um SQL-DMO **SQLServer** objeto usando sua ProgID.  
  
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
 O exemplo a seguir cria um SQL-DMO **SQLServer** objeto usando sua CLSID.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [OLE procedimentos armazenados de automação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Opção de configuração de servidor OLE Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)   
 [Script de exemplo de automação](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
