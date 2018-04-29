---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f3996455b61bfbe0bffe9e7199f5ecf87d4690a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Faz com que a execução de um pacote seja pausada e crie um arquivo de despejo. O arquivo está armazenado na pasta *\<unidade>*:\Arquivos de Programas\Microsoft SQL Server\130\Shared\ErrorDumps.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 A ID da execução do pacote em execução. O *execution_id* é **bigint**.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o pacote em execução com uma ID de execução de 88 é solicitado a criar um arquivo de despejo.  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (êxito)  
  
 Quando há falha no procedimento armazenado, ele gera um erro.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige que os usuários sejam membros da função de banco de dados **ssis_admin**.  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 A lista a seguir descreve as condições que podem provocar falha no procedimento armazenado.  
  
-   Uma ID de execução inválida é especificada.  
  
-   O pacote já foi concluído.  
  
-   O pacote está criando um arquivo de despejo no momento.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerar arquivos de despejo para execução de pacote](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
