---
title: Propriedades do banco de dados (página Opções) | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
caps.latest.revision: 67
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c357485b0e482dec6a0d81dfe9fca51676b03fb9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32932531"
---
# <a name="database-properties-options-page"></a>Propriedades do banco de dados (página Opções)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use esta página para exibir ou modificar opções para o banco de dados selecionado. Para obter mais informações sobre as opções disponíveis nessa página, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).  
  
## <a name="page-header"></a>Cabeçalho de página  
 **Agrupamento**  
 Especifique o agrupamento do banco de dados selecionando na lista. Para saber mais, veja [Set or Change the Database Collation](../../relational-databases/collations/set-or-change-the-database-collation.md).  
  
 **Modelo de recuperação**  
 Especifique um dos seguintes modelos para recuperar o banco de dados: **Full**, **Bulk-Logged**ou **simples**. Para obter mais informações sobre modelos de recuperação, veja [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
 **Nível de compatibilidade**  
 Especifique a última versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceita pelo banco de dados. Para obter os valores possíveis, consulte [Nível de compatibilidade ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md). Quando um banco de dados do SQL Server é atualizado, o nível de compatibilidade de banco de dados é mantido se possível ou alterado para o nível mínimo com suporte para o novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
 **Tipo de contenção**  
 Não especifique nada ou parcial para designar se este é um banco de dados independente. Para obter mais informações sobre bancos de dados independentes, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md). A propriedade de servidor **Habilitar Bancos de Dados Independentes** deve ser definida como **TRUE** antes que um banco de dados possa ser configurado como independente.  
  
> [!IMPORTANT]  
>  Habilitar delegados de bancos de dados parcialmente independentes controla o acesso à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os proprietários do banco de dados. Para obter mais informações, consulte [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="automatic"></a>Automatic  
 **Fechamento Automático**  
 Especifique se o banco de dados é fechado corretamente e libera recursos depois da saída do último usuário. Os valores possíveis são **True** e **False**. Quando **True**, o banco de dados é desligado corretamente e seus recursos são liberados depois do logoff do último usuário.  
  
 **Estatísticas incrementais de criação automática**  
 Especifique se você deseja usar a opção incremental durante a criação de estatísticas por partição. Para obter informações sobre estatísticas incrementais, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
 **Criar Estatísticas Automaticamente**  
 Especifique se o banco de dados cria automaticamente estatísticas de otimização ausentes. Os valores possíveis são **True** e **False**. Quando **True**, todas as estatísticas ausentes necessárias a uma consulta para otimização são criadas automaticamente durante a otimização. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
 **Reduzir Automaticamente**  
 Especifique se os arquivos do banco de dados estão disponíveis para redução periódica. Os valores possíveis são **True** e **False**. Para saber mais, veja [Shrink a Database](../../relational-databases/databases/shrink-a-database.md).  
  
 **Atualização Automática de Estatísticas**  
 Especifique se o banco de dados atualiza estatísticas de otimização desatualizadas automaticamente. Os valores possíveis são **True** e **False**. Quando definidas como **True**, todas as estatísticas desatualizadas necessárias à consulta para otimização são criadas automaticamente durante a otimização. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
 **Atualização Automática de Estatísticas de Forma Assíncrona**  
 Quando definidas como **True**, as consultas que iniciam uma atualização automática de estatísticas desatualizadas não aguardam que as estatísticas sejam atualizadas antes da compilação. Consultas subsequentes usam as estatísticas atualizadas quando elas estiverem disponíveis.  
  
 Quando definidas como **False**, as consultas que iniciam uma atualização automática de estatísticas desatualizadas aguardarão até que as estatísticas possam ser usadas no plano de otimização da consulta.  
  
 A configuração dessa opção como **True** não tem nenhum efeito, salvo se **Atualização Automática de Estatísticas** também estiver definida como **True**.  
  
## <a name="containment"></a>Containment  
 Nos bancos de dados independentes, algumas configurações geralmente definidas no nível de servidor podem ser configuradas no nível de banco de dados.  
  
 **LCID do Idioma de Texto Completo Padrão**  
 Especifica um idioma padrão para colunas indexadas de texto completo. A análise linguística dos dados indexados de texto completo depende do idioma dos dados. O valor padrão dessa opção é o idioma do servidor. Para obter a linguagem que corresponde à configuração exibida, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
 **Idioma Padrão**  
 O idioma padrão para todos os novos usuários de bancos de dados independentes, a menos que especificado de outra maneira.  
  
 **Gatilhos Aninhados Habilitados**  
 Permite que gatilhos acionem outros gatilhos. Os gatilhos podem ser aninhados até no máximo 32 níveis. Para obter mais informações, confira a seção “Gatilhos aninhados” em [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 **Transformar Palavras de Ruído**  
 Suprima uma mensagem de erro se palavras de ruído ou palavras irrelevantes farão uma operação Booliana em uma consulta de texto completo retornar zero linha. Para saber mais, veja [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  
 **Corte de Ano de Dois Dígitos**  
 Indica o número de ano mais alto que pode ser digitado como um ano de dois dígitos. O ano listado e os 99 anos anteriores podem ser digitados como um ano de dois dígitos. Todos os outros anos devem ser digitados como um ano de quatro dígitos.  
  
 Por exemplo, a configuração padrão de 2049 indica que a data digitada como ‘14/3/49’ será interpretada como 14 de março de 2049 e a data digitada como ‘14/3/50’ será interpretada como 14 de março de 1950. Para saber mais, veja [Configure the two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="cursor"></a>Cursor  
 **Fechar Cursor Quando a Confirmação for Habilitada**  
 Especifique se os cursores são fechados após a confirmação da transação que abre o cursor. Os valores possíveis são **True** e **False**. Quando **True**, todos os cursores abertos quando uma transação for confirmada ou revertida serão fechados. Quando **False**, esses cursores permanecerão abertos quando uma transação for confirmada. Quando **False**, a reversão de uma transação fecha todos os cursores, exceto os definidos como INSENSITIVE ou STATIC. Para obter mais informações, veja [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md).  
  
 **Cursor Padrão**  
 Especifique o comportamento padrão do cursor. Quando **True**, as declarações de cursor são padronizadas como LOCAL. Quando **False**, os cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] são padronizados como GLOBAL.  
  
## <a name="database-scoped-configurations"></a>Configurações no Escopo do Banco de Dados  
 No SQL Server 2016 e no Banco de Dados SQL do Azure, há várias propriedades de configuração que podem ser definidas para o nível de banco de dados. Para obter mais informações sobre todas essas configurações, veja [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).  
  
 **Estimativa de cardinalidade herdada**  
 Especifique o modelo de estimativa de cardinalidade do otimizador de consulta para o primário, independentemente do nível de compatibilidade do banco de dados. Isso é equivalente ao [Sinalizador de Rastreamento 9481](https://support.microsoft.com/en-us/kb/2801413).  
  
 **Estimativa de cardinalidade herdada para secundário**  
 Especifique o modelo de estimativa de cardinalidade do otimizador de consulta para os secundários, se houver, independentemente do nível de compatibilidade do banco de dados. Isso é equivalente ao [Sinalizador de Rastreamento 9481](https://support.microsoft.com/en-us/kb/2801413).  
  
 **DOP Máximo**  
 Especifique a configuração padrão [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) para o primário que deve ser usado para as instruções.  
  
 **DOP Máximo para Secundário**  
 Especifique a configuração padrão [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) para os secundários, se houver, que devem ser usados para as instruções.  
  
 **Detecção de parâmetros**  
 Habilita ou desabilita o parâmetro de detecção no primário. Isso é equivalente ao [Sinalizador de Rastreamento 4136](https://support.microsoft.com/en-us/kb/980653).  
  
 **Detecção de Parâmetros para Secundário**  
 Habilita ou desabilita a detecção de parâmetros em secundários, se houver. Isso é equivalente ao [Sinalizador de Rastreamento 4136](https://support.microsoft.com/en-us/kb/980653).  
  
 **Correções do otimizador de consulta**  
 Habilita ou desabilita os hotfixes de otimização da consulta primária, independentemente do nível de compatibilidade do banco de dados. Isso é equivalente ao [Sinalizador de Rastreamento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
 **Correções do otimizador de consulta para secundário**  
 Habilita ou desabilita os hotfixes de otimização da consulta em secundários, independentemente do nível de compatibilidade do banco de dados. Isso é equivalente ao [Sinalizador de Rastreamento 4199](https://support.microsoft.com/en-us/kb/974006).  
  
## <a name="filestream"></a>FILESTREAM  
 **Nome do Diretório FILESTREAM**  
 Especifique o nome de diretório para obter os dados FILESTREAM associados ao banco de dados selecionado.  
  
 **Acesso Não Transacionado a FILESTREAM**  
 Especifique uma das seguintes opções para acesso não transacional através do sistema de arquivos aos dados FILESTREAM armazenados em FileTables: **OFF**, **READ_ONLY**ou **FULL**. Se FILESTREAM não estiver habilitado no servidor, esse valor será definido como OFF e será desabilitado. Para obter mais informações, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
## <a name="miscellaneous"></a>Diversos  
**Permitir o isolamento de instantâneo**  
Habilita esse recurso.  

 **Padrão ANSI NULL**  
 Permita valores nulos para todos os tipos de dados ou colunas definidos pelo usuário que não estejam explicitamente definidos como **NOT NULL** durante uma instrução **CREATE TABLE** ou **ALTER TABLE** (o estado padrão). Para obter mais informações, veja [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md) e [SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md).  
  
 **ANSI NULLS Habilitado**  
 Especifique o comportamento dos operadores de comparação Igual a (`=`) e Diferente de (`<>`) quando usados com valores nulos. Os valores possíveis são **True** (ativado) e **False** (desativado). Quando **True**, todas as comparações com um valor nulo são avaliadas como UNKNOWN. Quando definidas como **False**, as comparações de valores não UNICODE com um valor nulo são avaliadas como **True** se os dois valores são NULL. Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 **Preenchimento ANSI Habilitado**  
 Especifique se preenchimento ANSI está ativado ou desativado. Os valores permitidos são **True** (ativado) e **False** (desativado). Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
 **Avisos ANSI Habilitados**  
 Especifique comportamento padrão ISO para várias condições de erro. Quando definida como **True**, uma mensagem de aviso será gerada se valores nulos aparecerem em funções de agregação (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP ou COUNT). Quando **False**, nenhum aviso é emitido. Para obter mais informações, veja [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).  
  
 **Anular Aritmética Habilitada**  
 Especifique se a opção de banco de dados de anulação de aritmética está habilitada ou não. Os valores possíveis são **True** e **False**. Quando definido como **True**, um estouro ou erro de divisão por zero faz com que a consulta ou o lote sejam encerrados. Se o erro ocorrer em uma transação, a transação será revertida. Quando **False**, uma mensagem de aviso será exibida, mas a consulta, o lote ou a transação continuará como se nenhum erro tivesse ocorrido. Para obter mais informações, veja [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).  
  
 **Concatenar Nulo Produz Nulo**  
 Especifique o comportamento quando valores nulos são concatenados. Quando o valor da propriedade é **True**, **string** + NULL retorna NULL. Quando **False**, o resultado é **string**. Para obter mais informações, veja [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
  
 **Encadeamento de Propriedades de Bancos de Dados**  
 Esse valor somente leitura indica se o encadeamento de propriedades de bancos de dados foi habilitado. Quando definido como **True**, o banco de dados pode ser a origem ou o destino de uma cadeia de propriedade de bancos de dados. Use a instrução ALTER DATABASE para definir essa propriedade.  
  
 **Otimização de Correlação de Data Habilitada**  
 Quando definido como **True**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém as estatísticas de correlação entre as duas tabelas do banco de dados que estiverem vinculadas por uma restrição FOREIGN KEY e possuírem colunas **datetime** .  
  
 Quando **False**, as estatísticas de correlação não são mantidas.  
 
 **Durabilidade atrasada**  
 Habilita esse recurso.  
 
 **O Instantâneo de Leitura Confirmada Está Ativo**  
 Habilita esse recurso.  
 
 **Anular Arredondamento Numérico**  
 Especifique como o banco de dados trata erros de arredondamento. Os valores possíveis são **True** e **False**. Quando **True**, um erro é gerado quando ocorrer perda de precisão em uma expressão. Quando **False**, perdas de precisão não geram mensagens de erro e o resultado é arredondado para a precisão da coluna ou variável que armazena o resultado. Para obter mais informações, veja [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md).  
  
 **Parametrização**  
 Quando definidas como **SIMPLE**, as consultas são parametrizadas com base no comportamento padrão do banco de dados. Quando **FORCED**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas as consultas no banco de dados.  
  
 **Identificadores entre Aspas Habilitados**  
 Especifique se palavras-chave do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser usadas como identificadores (um nome de variável ou objeto) se estiverem incluídas entre aspas. Os valores possíveis são **True** e **False**. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 **Gatilhos Recursivos Habilitados**  
 Especifique se gatilhos podem ser acionados por outros gatilhos. Os valores possíveis são **True** e **False**. Quando definido como **True**, essa opção habilita o acionamento recursivo de gatilhos. Quando definido como **False**, apenas recursão direta é evitada. Para desabilitar a recursão indireta, defina a opção de servidor nested triggers como 0 usando sp_configure. Para obter mais informações, consulte [Criar gatilhos aninhados](../../relational-databases/triggers/create-nested-triggers.md).  
  
 **Confiável**  
 Quando exibe **True**, essa opção somente leitura indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite acesso a recursos fora do banco de dados em um contexto de representação estabelecido dentro do banco de dados. Contextos de representação podem ser estabelecidos dentro do banco de dados usando a instrução de usuário EXECUTE AS ou a cláusula EXECUTE AS em módulos do banco de dados.  
  
 Para ter acesso, o proprietário do banco de dados também precisa ter a permissão AUTHENTICATE SERVER no nível do servidor.  
  
 Essa propriedade também permite criação e execução de assemblies de acesso inseguros e externos dentro do banco de dados. Além disso, para configurar essa propriedade como **True**, o proprietário do banco de dados deve ter a permissão EXTERNAL ACCESS ASSEMBLY ou UNSAFE ASSEMBLY no nível do servidor.  
  
 Por padrão, todos os bancos de dados do usuário e todos os bancos de dados do sistema (com exceção do **MSDB**) têm essa propriedade definida como **False**. O valor não pode ser alterado para os bancos de dados **modelo** e **tempdb** .  
  
 TRUSTWORTHY é definido como **False** sempre que um banco de dados está conectado ao servidor.  
  
 A abordagem recomendada para acessar recursos fora do banco de dados em um contexto de representação é usar certificados e assinaturas em vez da opção **Trustworthy** .  
  
 Para definir essa propriedade, use a instrução ALTER DATABASE.  
  
 **Formato de Armazenamento VarDecimal Habilitado**  
 Essa opção é somente leitura a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Quando **True**, este banco de dados está habilitado para o formato de armazenamento vardecimal. O formato de armazenamento vardecimal não pode ser desabilitado enquanto qualquer tabela do banco de dados o estiver usando. No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores, todos os bancos de dados são habilitados para o formato de armazenamento. Essa opção usa [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md).  
  
## <a name="recovery"></a>Recuperação  
 **Verificação de Página**  
 Especifique a opção usada para descobrir e relatar transações de E/S incompletas provocadas por erros de E/S em disco. Os valores possíveis são **Nenhum**, **TornPageDetection**e **Soma de Verificação**. Para obter mais informações, veja [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
 **Tempo de Recuperação de Destino (Segundos)**  
 Especifica o salto máximo no tempo, expresso em segundos, para recuperar o banco de dados especificado no caso de uma falha. Para obter mais informações, consulte [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  

## <a name="service-broker"></a>Service Broker  
**Agente Habilitado**  
Habilita ou desabilita o Service Broker.  

**Honrar Prioridade do Agente**  
Propriedade do Service Broker somente leitura.  

**Identificador do Service Broker**  
Identificador somente leitura.  

## <a name="state"></a>Estado  
 **Banco de Dados Somente Leitura**  
 Especifique se o banco de dados é somente leitura. Os valores possíveis são **True** e **False**. Quando **True**, os usuários podem apenas ler dados no banco de dados. Os usuários não podem modificar os dados ou objetos de banco de dados. No entanto, o próprio banco de dados pode ser excluído usando a instrução `DROP DATABASE`. O banco de dados não pode estar em uso quando um novo valor para a opção **Banco de Dados Somente Leitura** estiver especificado. O banco de dados mestre é a exceção e só o administrador do sistema pode usar o mestre enquanto a opção estiver sendo definida.  
  
 **Estado do Banco de Dados**  
 Exiba o estado atual do banco de dados. Não é editável. Para obter mais informações sobre o **Estado do Banco de Dados**, consulte [Database States](../../relational-databases/databases/database-states.md)  

 **Criptografia Habilitada**  
 Quando definido como **True**, esse banco de dados está habilitado para criptografia de banco de dados. Uma Chave de Criptografia do Banco de Dados é necessária para criptografia. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
 **Acesso Restrito**  
 Especifique quais usuários podem acessar o banco de dados. Os valores possíveis são:  
  
-   **Vários**  
  
     O estado normal de um banco de dados de produção. Permite que vários usuários acessem o banco de dados de uma vez.  
  
-   **Single**  
  
     Usado para ações de manutenção, apenas um usuário tem permissão para acessar o banco de dados por vez.  
  
-   **Restricted**  
  
     Apenas membros das funções db_owner, dbcreator ou sysadmin podem usar o banco de dados.  
  


## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
