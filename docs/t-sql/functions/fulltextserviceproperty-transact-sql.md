---
title: FULLTEXTSERVICEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXTSERVICEPROPERTY_TSQL
- FULLTEXTSERVICEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- FULLTEXTSERVICEPROPERTY function
- services [SQL Server], full-text search properties
- test
ms.assetid: b7dcacb0-af83-4807-9d1e-49148b56b59c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4fbdc84168ea3c0878924033347ca0c0fff3e514
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206155"
---
# <a name="fulltextserviceproperty-transact-sql"></a>FULLTEXTSERVICEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações relacionadas às propriedades do Mecanismo de Texto Completo. Essas propriedades podem ser definidas e recuperadas usando **sp_fulltext_service**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FULLTEXTSERVICEPROPERTY ('property')  
```  
  
## <a name="arguments"></a>Argumentos  
 *property*  
 É uma expressão contendo o nome da propriedade em nível de serviço de texto completo. A tabela lista as propriedades e fornece descrições das informações retornadas.  
  
> [!NOTE]
>  Essa coluna será removida em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **ConnectTimeout**, **DataTimeout** e **ResourceUsage**. Evite usá-las em um novo projeto de desenvolvimento e planeje a modificação dos aplicativos que as utilizam atualmente.  
  
|Propriedade|Valor|  
|--------------|-----------|  
|**ResourceUsage**|Retorna 0. Com suporte somente para compatibilidade com versões anteriores.|  
|**ConnectTimeout**|Retorna 0. Com suporte somente para compatibilidade com versões anteriores.|  
|**IsFulltextInstalled**|O componente de texto completo é instalado com a instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Texto completo não é instalado.<br /><br /> 1 = Texto completo é instalado.<br /><br /> NULL = Entrada inválida ou erro.|  
|**DataTimeout**|Retorna 0. Com suporte somente para compatibilidade com versões anteriores.|  
|**LoadOSResources**|Indica se os separadores de palavra e filtros do sistema operacional estão registrados e são usados com essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, esta propriedade é desabilitada para evitar alterações de comportamento inadvertido em atualizações feitas no sistema operacional. Habilitar o uso de recursos do sistema operacional fornece acesso a recursos para idiomas e tipos de documentos registrados no Serviço de Indexação [!INCLUDE[msCoName](../../includes/msconame-md.md)], mas que tenha um recurso especifico de instância instalado. Ao habilitar o carregamento de recursos do sistema operacional, verifique se eles são recursos binários assinados confiáveis. Caso contrário, não poderão ser carregados quando o **VerifySignature** for definido como 1.<br /><br /> 0 = Usa somente filtros e separadores de palavra específicos para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Carrega filtros e separadores de palavra do sistema operacional.|  
|**VerifySignature**|Especifica se somente binários assinados são carregados pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search Service. Por padrão, somente binários assinados confiáveis são carregados.<br /><br /> 0 = Não verifica se binários são assinados.<br /><br /> 1 = Verifica se somente binários assinados confiáveis são carregados.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir verifica se somente binários assinados são carregados e o valor de retorno indica que esta verificação não está sendo feita.  
  
```  
SELECT fulltextserviceproperty('VerifySignature');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
0  
```  
  
 Saiba que para definir a verificação de assinatura novamente para seu valor padrão, 1, você pode usar a seguinte instrução `sp_fulltext_service`:  
  
```  
EXEC sp_fulltext_service @action='verify_signature', @value=1;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
  
