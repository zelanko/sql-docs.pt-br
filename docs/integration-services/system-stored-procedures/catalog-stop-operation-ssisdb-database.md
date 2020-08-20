---
description: catalog.stop_operation (Banco de Dados SSISDB)
title: catalog.stop_operation (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 97fd9d22-03dd-4eda-8f6c-ba8b67acec68
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c77113417a108632aab150e75011399f9ad3a752
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477073"
---
# <a name="catalogstop_operation-ssisdb-database"></a>catalog.stop_operation (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Para uma validação ou instância de execução no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @operation_id = ] *operation_id*  
 O Identificador exclusivo da validação ou da instância de execução. O *operation_id* é **bigint**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   permissões READ e MODIFY na validação ou instância de execução  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve algumas condições que podem gerar um erro ou um aviso:  
  
-   O usuário não tem as permissões apropriadas  
  
-   O identificador da operação não é válido  
  
-   A operação já foi interrompida  
  
## <a name="remarks"></a>Comentários  
 Somente um usuário deve parar uma operação por vez no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se vários usuários tentarem parar a operação, o procedimento armazenado retornará com êxito (o valor `0`) na primeira tentativa, mas nas tentativas subsequentes, será gerado um erro.  
  
  
