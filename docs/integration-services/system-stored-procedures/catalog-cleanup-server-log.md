---
title: catalog.cleanup_server_log | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0dedb685-d3a6-4bd6-8afd-58d98853deee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b80b346c426ae68a1c6b0750bca112417861f51e
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288070"
---
# <a name="catalogcleanup_server_log"></a>catalog.cleanup_server_log 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Limpa os logs de operação para levar o banco de dados SSISDB a um estado que permite a alteração do valor da propriedade SERVER_OPERATION_ENCRYPTION_LEVEL.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
catalog.cleanup_server_log  
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 para êxito e 1 para falha.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
  
-   Permissões READ e EXECUTE no projeto e, se aplicável, permissões READ no ambiente referenciado.  
  
-   Associação na função de banco de dados **ssis_admin**.  
  
-   Associação à função de servidor **sysadmin**.  
  
## <a name="errors-and-warnings"></a>Erros e avisos  
 Esse procedimento armazenado gera erros nos seguintes cenários:  
  
-   Há uma ou mais operações ativas no banco de dados SSISDB.  
  
-   O banco de dados SSISDB não está no modo de usuário único.  
  
## <a name="remarks"></a>Comentários  
 SQL Server 2012 Service Pack 2 adicionou a propriedade SERVER_OPERATION_ENCRYPTION_LEVEL à tabela **internal.catalog_properties**. Essa propriedade tem dois valores possíveis:  
  
-   **PER_EXECUTION (1)** – O certificado e a chave simétrica usados para proteger parâmetros de execução e logs de execução confidenciais são criados para cada execução. Você pode ter problemas de desempenho (deadlocks, trabalhos de manutenção com falha, etc.) em um ambiente de produção porque chaves/certificado são gerados para cada execução. No entanto, essa configuração fornece um nível maior de segurança que o outro valor (2).  
  
-   **PER_PROJECT (2)** – O certificado e a chave simétrica usados para proteger parâmetros confidenciais são criados para cada projeto. PER_PROJECT (2) é o valor padrão. Essa configuração oferece um desempenho melhor do que o nível PER_EXECUTION porque a chave e o certificado são gerados uma vez para um projeto em vez de serem gerados para cada execução.  
  
 Você precisa executar o procedimento armazenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md) antes de alterar o SERVER_OPERATION_ENCRYPTION_LEVEL de 2 para 1 ou de 1 para 2. Você precisa fazer o seguinte antes de executar este procedimento armazenado:  
  
1.  Verifique se o valor da propriedade OPERATION_CLEANUP_ENABLED está definido como TRUE na tabela [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
2.  Defina o SSISDB (banco de dados do Integration Services) para o modo de usuário único. No SQL Server Management Studio, inicie a caixa de diálogo Propriedades do Banco de Dados do SSISDB, mude para a guia Opções e defina a propriedade Restringir Acesso para o modo de usuário único (SINGLE_USER). Depois de executar o procedimento armazenado cleanup_server_log, defina o valor da propriedade para o valor original.  
  
3.  Execute o procedimento armazenado [catalog.cleanup_server_log](../../integration-services/system-stored-procedures/catalog-cleanup-server-log.md).  
  
4.  Agora, vá em frente e altere o valor da propriedade SERVER_OPERATION_ENCRYPTION_LEVEL na tabela [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
5.  Execute o procedimento armazenado [catalog.cleanup_server_execution_keys](../../integration-services/system-stored-procedures/catalog-cleanup-server-execution-keys.md) para limpar as chaves de certificado do banco de dados SSISDB. Descartar certificados e chaves de banco de dados SSISDB pode levar muito tempo, então isso deve ser executado periodicamente fora dos horários de pico.  
  
     Você pode especificar o escopo ou o nível (execução versus projeto) e o número de chaves a serem excluídas. O tamanho de lote padrão para exclusão é 1000. Quando você define o nível para 2, as chaves e certificados serão excluídos somente se os projetos associados foram excluídos.  
  
 Para obter mais informações, veja o artigo da Base de Dados de Conhecimento a seguir: [CORREÇÃO: problemas de desempenho ao usar o SSISDB como o repositório de implantação no SQL Server 2012](https://support.microsoft.com/kb/2972285)  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir chama o procedimento armazenado cleanup_server_log.  
  
```sql  
USE [SSISDB]  
GO  
  
DECLARE@return_value int  
EXEC@return_value = [internal].[cleanup_server_log]  
SELECT'Return Value' = @return_value  
GO   
```  
  
  
