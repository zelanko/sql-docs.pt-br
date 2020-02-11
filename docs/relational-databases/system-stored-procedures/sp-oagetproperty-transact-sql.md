---
title: sp_OAGetProperty (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6efc0b620dcec300b5342ea5a0f63358fcdfadc5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107886"
---
# <a name="sp_oagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Obtém um valor de propriedade de um objeto OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 É o token do objeto de um objeto OLE criado anteriormente usando **sp_OACreate**.  
  
 *propertyname*  
 É o nome de propriedade do objeto OLE a ser retornado.  
  
 *PropertyValue* de **saída**  
 É o valor de propriedade retornado. Se for especificado, deverá ser uma variável local do tipo de dados apropriado.  
  
 Se a propriedade retornar um objeto OLE, *PropertyValue* deverá ser uma variável local do tipo de dados **int**. Um token de objeto é armazenado na variável local e esse token de objeto pode ser usado com outros procedimentos armazenados de automação OLE.  
  
 Se a propriedade retornar um único valor, especifique uma variável local para *PropertyValue*, que retorna o valor da propriedade na variável local; ou não especifique *PropertyValue*, que retorna o valor da propriedade para o cliente como um conjunto de resultados de coluna única e de linha única.  
  
 Quando a propriedade retorna uma matriz, se *PropertyValue* for especificado, ela será definida como NULL.  
  
 Se *PropertyValue* for especificado, mas a propriedade não retornar um valor, ocorrerá um erro. Se a propriedade retornar uma matriz com mais de duas dimensões, ocorrerá um erro.  
  
 *index*  
 É um parâmetro de índice. Se especificado, o *índice* deve ser um valor do tipo de dados apropriado.  
  
 Algumas propriedades têm parâmetros. Estas propriedades são chamadas de propriedades indexadas e os parâmetros são chamados de parâmetros de índice. Uma propriedade pode ter vários parâmetros de índice.  
  
> [!NOTE]  
>  Os parâmetros deste procedimento armazenado são especificados por posição, não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [códigos de retorno de automação OLE e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se a propriedade retornar uma matriz com uma ou duas dimensões, a matriz será retornada ao cliente como um conjunto de resultados:  
  
-   Uma matriz unidimensional é retornada ao cliente como um conjunto de resultados de uma linha, com tantas colunas quanto houver elementos na matriz. Em outras palavras, a matriz é retornada como colunas.  
  
-   Uma matriz bidimensional é retornada ao cliente como um conjunto de resultados com tantas colunas quanto houver elementos na primeira dimensão da matriz e com tantas linhas quanto houver elementos na segunda dimensão da matriz. Em outras palavras, a matriz é retornada como (colunas, linhas).  
  
 Quando um valor de retorno de propriedade ou um valor de retorno de método é uma matriz, **sp_OAGetProperty** ou **sp_OAMethod** retorna um conjunto de resultados para o cliente. (Os parâmetros de saída de método não podem ser matrizes.) Esses procedimentos examinam todos os valores de dados na matriz para determinar os tipos de dados apropriados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tamanhos dos dados a serem usados para cada coluna no conjunto de resultados. Para uma coluna específica, esses procedimentos usam o tipo de dados e o tamanho necessários para representar todos os valores de dados nesta coluna.  
  
 Quando todos os valores de dados em uma coluna compartilharem o mesmo tipo de dados, esse tipo de dados será usado para a coluna inteira. Quando os valores de dados em uma coluna forem de tipos de dados diferentes, o tipo de dados da coluna inteira será escolhido com base no quadro a seguir.  
  
||INT|FLOAT|money|DATETIME|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Comentários  
 Você também pode usar **sp_OAMethod** para obter um valor de propriedade.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** ou a permissão execute diretamente neste procedimento armazenado. `Ole Automation Procedures`a configuração deve ser **habilitada** para usar qualquer procedimento do sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-local-variable"></a>a. Usando uma variável local  
 O exemplo a seguir obtém `HostName` a propriedade (do objeto **SqlServer** criado anteriormente) e a armazena em uma variável local.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. Usando um conjunto de resultados  
 O exemplo a seguir obtém `HostName` a propriedade (do objeto **SqlServer** criado anteriormente) e a retorna ao cliente como um conjunto de resultados.  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
