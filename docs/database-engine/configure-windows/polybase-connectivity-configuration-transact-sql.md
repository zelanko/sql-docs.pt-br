---
title: Configuração de conectividade do PolyBase (Transact-SQL) | Microsoft Docs
description: Descubra como usar o sp_configure para exibir ou alterar as definições da configuração global para o PolyBase Hadoop e a conectividade do Armazenamento de Blobs do Azure.
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: polybase
ms.topic: reference
helpviewer_keywords:
- PolyBase
ms.assetid: 82252e4f-b1d0-49e5-aa0b-3624aade2add
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b3daf000381fbfaa5481ae18f348bd987689e46b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938937"
---
# <a name="polybase-connectivity-configuration-transact-sql"></a>Configuração de conectividade do PolyBase (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-pdw-md.md)]

  Exibe ou altera as definições de configurações globais para o PolyBase Hadoop e a conectividade do armazenamento de blobs do Azure.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@configname=** ] **'** _option\_name_ **'**  
 É o nome de uma opção de configuração. *option_name* é **varchar(35)** , com um padrão de NULL. Se não for especificado, a lista completa de opções será retornada.  
  
 [ **@configvalue=** ] **'** _value_ **'**  
 É a nova definição de configuração. *value* é **int**, com um padrão NULL. O valor máximo depende da opção individual.  
  
 **'conectividade do hadoop'**  
 Especifica o tipo de fonte de dados do Hadoop para todas as conexões do PolyBase com clusters Hadoop ou com o armazenamento de blobs do Azure (WASB). Essa configuração é necessária para criar uma fonte de dados externa para uma tabela externa. Para obter mais informações, confira [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md),  
  
 Estas são as configurações de conectividade do Hadoop e suas fontes de dados Hadoop com suporte correspondentes. Somente uma configuração pode estar em vigor por vez. As opções 1, 4 e 7 permitem a criação e uso de vários tipos de fontes de dados externas em todas as sessões no servidor.  
  
-   Opção 0: Desabilitar a conectividade do Hadoop  
  
-   Opção 1: Hortonworks HDP 1.3 no Windows Server  
  
-   Opção 1: Armazenamento de Blobs do Azure (WASB[S])  
  
-   Opção 2: Hortonworks HDP 1.3 no Linux  
  
-   Opção 3: Cloudera CDH 4.3 em Linux  
  
-   Opção 4: Hortonworks HDP 2.0 no Windows Server  
  
-   Opção 4: Armazenamento de Blobs do Azure (WASB[S])  
  
-   Opção 5: Hortonworks HDP 2.0 no Linux  
  
-   Opção 6: Cloudera 5.1, 5.2, 5.3, 5.4, 5.5, 5.9, 5.10, 5.11, 5.12 e 5.13 no Linux  
  
-   Opção 7: Hortonworks 2.1, 2.2, 2.3, 2.4, 2.5, 2.6, 3.0 no Linux  
  
-   Opção 7: Hortonworks 2.1, 2.2 e 2.3 no Windows Server  
  
-   Opção 7: Armazenamento de Blobs do Azure (WASB[S])  
  
 **RECONFIGURE**  
 Atualiza o valor de execução (run_value) para corresponder ao valor de configuração (config_value). Confira [Result Sets](#ResultSets) para obter as definições de run_value e config_value. O novo valor de configuração definido por sp_configure não entra em vigor até que o valor de execução seja definido pela instrução RECONFIGURE.  
  
 Após executar RECONFIGURE, você deve parar e reiniciar o serviço SQL Server. Observe que ao interromper o serviço SQL Server, o Mecanismo PolyBase e o Serviço de Movimentação de Dados adicionais serão interrompidos automaticamente. Depois de reiniciar o serviço do mecanismo SQL Server, reinicie esses dois serviços novamente (eles não serão iniciados automaticamente).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
##  <a name="result-sets"></a><a name="ResultSets"></a> Result Sets  
 Quando é executado sem parâmetros, **sp_configure** retorna um conjunto de resultados com cinco colunas.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(35)**|O nome da opção de configuração.|  
|**minimum**|**int**|Valor mínimo da opção de configuração.|  
|**maximum**|**int**|Valor máximo da opção de configuração.|  
|**config_value**|**int**|Valor definido usando **sp_configure**.|  
|**run_value**|**int**|O valor atual que está sendo usado pelo PolyBase. Esse valor é definido pela execução de RECONFIGURE.<br /><br /> Normalmente, **config_value** e **run_value** são os mesmos, a menos que o valor esteja sendo alterado.<br /><br /> Talvez seja necessário reinicializar antes que esse valor de execução seja preciso, caso a reconfiguração esteja em andamento.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Após a execução de RECONFIGURE no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que o valor de execução de 'conectividade do hadoop' entre em vigor, é necessário reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
Após a execução de RECONFIGURE no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], para que o valor de execução de 'conectividade do hadoop' entre em vigor, é necessário reiniciar a região [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 RECONFIGURE não é permitido em uma transação explícita ou implícita.  
  
## <a name="permissions"></a>Permissões  
 Todos os usuários podem executar **sp_configure** sem parâmetros ou com o parâmetro @configname .  
  
 Exige a permissão no nível do servidor **ALTER SETTINGS** ou a associação à função de servidor fixa **sysadmin** para alterar um valor de configuração ou para executar RECONFIGURE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-list-all-available-configuration-settings"></a>a. Listar todas as configurações disponíveis  
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
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
