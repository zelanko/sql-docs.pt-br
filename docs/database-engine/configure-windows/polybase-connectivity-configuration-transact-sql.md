---
title: "Configuração de conectividade do PolyBase (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 74f73ab33a010583b4747fcc2d9b35d6cdea14a2
ms.openlocfilehash: b57b1e802969995f87d5663e5e7dbdc92700a9b5
ms.contentlocale: pt-br
ms.lasthandoff: 08/04/2017

---
# <a name="polybase-connectivity-configuration-transact-sql"></a>Configuração de conectividade do PolyBase (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-pdw-md.md)]

  Exibe ou altera as definições de configurações globais para o PolyBase Hadoop e a conectividade do armazenamento de blobs do Azure.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
--List all of the configuration options  
sp_configure  
[;]  
  
--Configure Hadoop connectivity  
sp_configure [ @configname = ] 'hadoop connectivity',  
             [ @configvalue = ] { 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 }  
[;]  
  
RECONFIGURE  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@configname=** ] **'***option_name***'**  
 É o nome de uma opção de configuração. *option_name* é **varchar(35)**, com um padrão de NULL. Se não for especificado, a lista completa de opções será retornada.  
  
 [ **@configvalue=** ] **'***value***'**  
 É a nova definição de configuração. *value* é **int**, com um padrão NULL. O valor máximo depende da opção individual.  
  
 **'conectividade do hadoop'**  
 Especifica o tipo de fonte de dados do Hadoop para todas as conexões do PolyBase com clusters Hadoop ou com o armazenamento de blobs do Azure (WASB). Essa configuração é necessária para criar uma fonte de dados externa para uma tabela externa. Para obter mais informações, confira [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md),  
  
 Estas são as configurações de conectividade do Hadoop e suas fontes de dados Hadoop com suporte correspondentes. Somente uma configuração pode estar em vigor por vez. As opções 1, 4 e 7 permitem a criação e uso de vários tipos de fontes de dados externas em todas as sessões no servidor.  
  
-   Opção 0: Desabilitar a conectividade do Hadoop  
  
-   Opção 1: Hortonworks HDP 1.3 no Windows Server  
  
-   Opção 1: Armazenamento de blobs do Azure (WASB[S])  
  
-   Opção 2: Hortonworks HDP 1.3 no Linux  
  
-   Opção 3: Cloudera CDH 4.3 no Linux  
  
-   Opção 4: Hortonworks HDP 2.0 no Windows Server  
  
-   Opção 4: armazenamento de blobs do Azure (WASB[S])  
  
-   Opção 5: Hortonworks HDP 2.0 no Linux  
  
-   Opção 6: Cloudera 5.1, 5.2, 5.3, 5.4, 5.5, 5.9, 5.10, 5.11 e 5.12 no Linux  
  
-   Opção 7: Hortonworks 2.1, 2.2, 2.3, 2.4, 2.5 e 2.6 no Linux  
  
-   Opção 7: Hortonworks 2.1, 2.2 e 2.3 no Windows Server  
  
-   Opção 7: armazenamento de blobs do Azure (WASB[S])  
  
 **RECONFIGURE**  
 Atualiza o valor de execução (run_value) para corresponder ao valor de configuração (config_value). Confira [Result Sets](#ResultSets) para obter as definições de run_value e config_value. O novo valor de configuração definido por sp_configure não entra em vigor até que o valor de execução seja definido pela instrução RECONFIGURE.  
  
 Após executar RECONFIGURE, você deve parar e reiniciar o serviço SQL Server. Observe que ao interromper o serviço SQL Server, o Mecanismo PolyBase e o Serviço de Movimentação de Dados adicionais serão interrompidos automaticamente. Depois de reiniciar o serviço do mecanismo SQL Server, reinicie esses dois serviços novamente (eles não serão iniciados automaticamente).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
##  <a name="ResultSets"></a> Result Sets  
 Quando é executado sem parâmetros, **sp_configure** retorna um conjunto de resultados com cinco colunas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|O nome da opção de configuração.|  
|**minimum**|**int**|Valor mínimo da opção de configuração.|  
|**maximum**|**int**|Valor máximo da opção de configuração.|  
|**config_value**|**int**|Valor definido usando **sp_configure**.|  
|**run_value**|**int**|O valor atual que está sendo usado pelo PolyBase. Esse valor é definido pela execução de RECONFIGURE.<br /><br /> Normalmente, **config_value** e **run_value** são os mesmos, a menos que o valor esteja sendo alterado.<br /><br /> Talvez seja necessário reinicializar antes que esse valor de execução seja preciso, caso a reconfiguração esteja em andamento.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Após a execução de RECONFIGURE no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que o valor de execução de 'conectividade do hadoop' entre em vigor, é necessário reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
Após a execução de RECONFIGURE no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], para que o valor de execução de 'conectividade do hadoop' entre em vigor, é necessário reiniciar a região [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 RECONFIGURE não é permitido em uma transação explícita ou implícita.  
  
## <a name="permissions"></a>Permissões  
 Todos os usuários podem executar **sp_configure** sem parâmetros ou com o parâmetro @configname .  
  
 Exige a permissão no nível do servidor **ALTER SETTINGS** ou a associação à função de servidor fixa **sysadmin** para alterar um valor de configuração ou para executar RECONFIGURE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-list-all-available-configuration-settings"></a>A. Listar todas as configurações disponíveis  
 O exemplo a seguir mostra como listar todas as opções de configuração.  
  
```  
EXEC sp_configure;  
```  
  
 O resultado retorna o nome da opção seguido pelos valores mínimo e máximo da opção. O **config_value** será o valor usado pelo SQL ou pelo PolyBase após a conclusão da reconfiguração. O **run_value** é o valor que está sendo usado. Normalmente, **config_value** e **run_value** são os mesmos, a menos que o valor esteja sendo alterado.  
  
### <a name="b-list-the-configuration-settings-for-one-configuration-name"></a>B. Listar as definições de configuração de um nome de configuração  
  
```  
EXEC sp_configure @configname='hadoop connectivity';  
```  
  
### <a name="c-set-hadoop-connectivity"></a>C. Definir a conectividade do Hadoop  
 Este exemplo define PolyBase para a opção 7. Essa opção permite que o PolyBase crie e use tabelas externas no Hortonworks 2.1, 2.2 e 2.3 no Linux e no Windows Server e no armazenamento de blobs do Azure. Por exemplo, o SQL pode ter 30 tabelas externas, com sete delas fazendo referência a dados no Hortonworks 2.1 no Linux, quatro no Hortonworks 2.2 no Linux, sete no Hortonworks 2.3 no Linux e os outros 12 fazendo referência ao armazenamento de blobs do Azure.  
  
```  
--Configure external tables to reference data on Hortonworks 2.1, 2.2, and 2.3 on Linux, and Azure blob storage  
  
sp_configure @configname = 'hadoop connectivity', @configvalue = 7;  
GO  
  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

