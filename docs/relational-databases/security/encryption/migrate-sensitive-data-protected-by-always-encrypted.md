---
title: Migrar dados confidenciais protegidos pelo Always Encrypted | Microsoft Docs
ms.custom: 
ms.date: 11/04/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fa13b882639b0b23d937c479eec6b2a29aa34ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>Migrar dados confidenciais protegidos pelo Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Para carregar dados criptografados sem realizar verificações de metadados no servidor durante operações de cópia em massa, crie o usuário com a opção **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS**. Essa opção destina-se a ser usada por ferramentas herdadas de versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] (como bcp.exe) ou ao usar fluxos de trabalho ETL (extrair, transformar, carregar) de terceiros que não podem usar o Always Encrypted. Isso permite que um usuário mova dados criptografados com segurança de um conjunto de tabelas, contendo colunas criptografadas, para outro conjunto de tabelas com colunas criptografadas (para o mesmo ou para outro banco de dados).  
 -  
 ## <a name="the-allowencryptedvaluemodifications-option"></a>A opção ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 Tanto [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) , quanto [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) tem uma opção ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Quando definida como ON (o padrão é OFF), essa opção suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa, o que permite ao usuário copiar em massa dados criptografados entre tabelas ou bancos de dados, sem descriptografá-los.  
  
## <a name="data-migration-scenarios"></a>Cenários de migração de dados  
A tabela a seguir mostra as configurações recomendadas apropriadas para vários cenários de migração.  
 
![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  

## <a name="bulk-loading-of-encrypted-data"></a>Carregamento em massa de dados criptografados  
Use o processo a seguir para carregar dados criptografados.  

1.  Defina a opção como ON para o usuário no banco de dados que é o alvo da operação de cópia em massa. Por exemplo:  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  Execute o aplicativo ou a ferramenta de cópia em massa que está se conectando como esse usuário. (Se seu aplicativo usa um driver de cliente habilitado para Always Encrypted, verifique se a cadeia de conexão da fonte de dados não contém **column encryption setting=enabled** , a fim de garantir que os dados recuperados da colunas criptografadas permanecem criptografados. Para obter mais informações, veja [Always Encrypted &#40;desenvolvimento de cliente&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md).)  
  
3.  Defina a opção ALLOW_ENCRYPTED_VALUE_MODIFICATIONS de volta para OFF. Por exemplo:  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>Possibilidade de dados corrompidos  
O uso inadequado dessa opção pode resultar em dados corrompidos. A opção **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** permite ao usuário inserir quaisquer dados nas colunas criptografadas do banco de dados, incluindo dados criptografados com chaves diferentes, incorretamente criptografados ou sem nenhuma criptografia. Se o usuário copiar acidentalmente os dados que não foram corretamente criptografados usando a configuração do esquema de criptografia (chave de criptografia de coluna, algoritmo, tipo de criptografia) para a coluna de destino, você não poderá descriptografar os dados (os dados serão corrompidos). Essa opção deve ser usada com cuidado, pois os dados poderão ser corrompidos no banco de dados.  

O cenário a seguir demonstra como importar dados incorretamente pode corromper os dados:  

1.  A opção está definida como ON para um usuário.  
 
2.  O usuário executa o aplicativo que se conecta ao banco de dados. O aplicativo usa APIs em massa para inserir valores de texto sem formatação às colunas criptografadas. O aplicativo espera um driver de cliente habilitado para o Always Encrypted a fim de criptografar os dados na inserção. No entanto, o aplicativo foi configurado incorretamente, de modo que ele acaba usando um driver que não é compatível com o Always Encrypted ou a cadeia de conexão não contém **column encryption setting=enabled**.  

3.  O aplicativo envia os valores de texto sem formatação ao servidor. Como as verificações de metadados criptográficos estão desabilitadas para o usuário no servidor, o servidor permite que os dados incorretos (texto sem formatação em vez de texto cifrado criptografado corretamente) sejam inseridos em uma coluna criptografada.  
 
4.  O mesmo ou outro aplicativo se conecta ao banco de dados usando o driver habilitado para o Always Encrypted e com **column encryption setting=enabled** na cadeia de conexão e recupera os dados. O aplicativo espera que os dados sejam descriptografados de maneira transparente. No entanto, o driver não descriptografa os dados porque trata-se de texto cifrado incorreto.  

## <a name="best-practice"></a>Prática recomendada  
 
Use contas de usuários designadas para execução longa de cargas de trabalho usando essa opção.  
 
Para aplicativos ou ferramentas de cópia em massa de execução curta que precisam mover dados criptografados sem descriptografá-los, defina a opção como ON imediatamente antes de executar o aplicativo e defini-lo de volta para OFF após a execução da operação.  
 
Não use essa opção para o desenvolvimento de novos aplicativos. Em vez disso, use um driver cliente (como ADO 4.6.1) que ofereça uma API para suprimir as verificações de metadados criptográficos de uma única sessão.  

## <a name="see-also"></a>Consulte também  
[CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
[ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
[Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Assistente de Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
[Always Encrypted &#40;desenvolvimento de cliente&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
