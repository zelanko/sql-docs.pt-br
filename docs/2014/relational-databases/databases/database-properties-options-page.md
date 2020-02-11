---
title: Propriedades do banco de dados (página Opções) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4420aaf7b11eccecf0b04bb67a55386215f1fc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62917077"
---
# <a name="database-properties-options-page"></a>Propriedades do banco de dados (página Opções)
  Use esta página para exibir ou modificar opções para o banco de dados selecionado. Para obter mais informações sobre as opções disponíveis nesta página, consulte [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="page-header"></a>Cabeçalho de página  
 **Ordenação**  
 Especifique a ordenação do banco de dados selecionando na lista. Para saber mais, veja [Definir ou alterar a ordenação de banco de dados](../collations/set-or-change-the-database-collation.md).  
  
 **Modelo de recuperação**  
 Especifique um dos seguintes modelos para recuperar o banco de dados: **Full**, **Bulk-Logged**ou **simples**. Para obter mais informações sobre modelos de recuperação, veja [Modelos de recuperação &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md).  
  
 **Nível de compatibilidade**  
 Especifique a última versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceita pelo banco de dados. Os valores possíveis são  **SQL Server 2014 (120)**,  **SQL Server 2012 (110)** e **SQL Server 2008 (100)**. Quando um banco de dados do SQL Server 2005 é atualizado para o SQL Server 2014, o nível de compatibilidade do banco de dados é alterado de 90 para 100.  O nível de compatibilidade 90 não tem suporte no SQL Server 2014. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
 **Tipo de contenção**  
 Não especifique nada ou parcial para designar se este é um banco de dados independente. Para obter mais informações sobre bancos de dados independentes, consulte [Contained Databases](contained-databases.md). A propriedade de servidor **Habilitar Bancos de Dados Independentes** deve ser definida como **TRUE** antes que um banco de dados possa ser configurado como independente.  
  
> [!IMPORTANT]  
>  Habilitar delegados de bancos de dados parcialmente independentes controla o acesso à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para os proprietários do banco de dados. Para obter mais informações, consulte [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md).  
  
## <a name="automatic"></a>Automático  
 **Fechamento automático**  
 Especifique se o banco de dados é fechado corretamente e libera recursos depois da saída do último usuário. Os valores possíveis são `True` e `False`. Quando `True`, o banco de dados é desligado corretamente e seus recursos são liberados depois do logoff do último usuário.  
  
 Estatísticas incrementais de criação automática  
 Especifique se você deseja usar a opção incremental durante a criação de estatísticas por partição. Para obter informações sobre estatísticas incrementais, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Criar estatísticas automaticamente**  
 Especifique se o banco de dados cria automaticamente estatísticas de otimização ausentes. Os valores possíveis são `True` e `False`. Quando `True`, quaisquer estatísticas ausentes exigidas pela consulta para otimização são criadas automaticamente durante a otimização. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Redução Automática**  
 Especifique se os arquivos do banco de dados estão disponíveis para redução periódica. Os valores possíveis são `True` e `False`. Para saber mais, veja [Shrink a Database](shrink-a-database.md).  
  
 **Atualizar estatísticas automaticamente**  
 Especifique se o banco de dados atualiza estatísticas de otimização desatualizadas automaticamente. Os valores possíveis são `True` e `False`. Quando `True`, quaisquer estatísticas desatualizadas exigidas pela consulta para otimização são criadas automaticamente durante a otimização. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Atualizar estatísticas automaticamente de forma assíncrona**  
 Quando `True`, as consultas que iniciam uma atualização automática de Estatísticas desatualizadas não aguardarão que as estatísticas sejam atualizadas antes da compilação. Consultas subsequentes usarão as estatísticas atualizadas quando elas estiverem disponíveis.  
  
 Quando `False`, as consultas que iniciam uma atualização automática de Estatísticas desatualizadas, esperam até que as estatísticas atualizadas possam ser usadas no plano de otimização de consulta.  
  
 Definir essa opção como `True` não tem efeito, a menos que as **Estatísticas de atualização automática** também sejam definidas como `True`.  
  
## <a name="containment"></a>Contenção  
 Nos bancos de dados independentes, algumas configurações geralmente definidas no nível de servidor podem ser configuradas no nível de banco de dados.  
  
 **LCID do idioma de texto completo padrão**  
 Especifica um idioma padrão para colunas indexadas de texto completo. A análise linguística dos dados indexados de texto completo depende do idioma dos dados. O valor padrão dessa opção é o idioma do servidor. Para obter a linguagem que corresponde à configuração exibida, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
 **Idioma padrão**  
 O idioma padrão para todos os novos usuários de bancos de dados independentes, a menos que especificado de outra maneira.  
  
 **Gatilhos aninhados habilitados**  
 Permite que gatilhos acionem outros gatilhos. Os gatilhos podem ser aninhados até no máximo 32 níveis. Para obter mais informações, confira a seção “Gatilhos aninhados” em [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Transformar palavras de ruído**  
 Suprima uma mensagem de erro se palavras de ruído ou palavras irrelevantes farão uma operação Booliana em uma consulta de texto completo retornar zero linha. Para saber mais, veja [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  
 **Corte de ano de dois dígitos**  
 Indica o número de ano mais alto que pode ser digitado como um ano de dois dígitos. O ano listado e os 99 anos anteriores podem ser digitados como um ano de dois dígitos. Todos os outros anos devem ser digitados como um ano de quatro dígitos.  
  
 Por exemplo, a configuração padrão de 2049 indica que a data digitada como ‘14/3/49’ será interpretada como 14 de março de 2049 e a data digitada como ‘14/3/50’ será interpretada como 14 de março de 1950. Para saber mais, veja [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="cursor"></a>Cursor  
 **Fechar cursor quando a confirmação estiver habilitada**  
 Especifique se os cursores são fechados após a confirmação da transação que abre o cursor. Os valores possíveis são `True` e `False`. Quando `True`, quaisquer cursores abertos quando uma transação for confirmada ou revertida serão fechados. Quando `False`, tais cursores permanecerão abertos quando uma transação for confirmada. Quando `False`, reverter uma transação fechará quaisquer cursores, exceto os definidos como INSENSITIVE ou STATIC. Para obter mais informações, veja [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql).  
  
 **Cursor padrão**  
 Especifique o comportamento padrão do cursor. Quando `True`, as declarações de cursor definem o padrão como LOCAL. Quando `False`, [!INCLUDE[tsql](../../includes/tsql-md.md)] cursores são padronizados como globais.  
  
## <a name="filestream"></a>FILESTREAM  
 **Nome do diretório FILESTREAM**  
 Especifique o nome de diretório para obter os dados FILESTREAM associados ao banco de dados selecionado.  
  
 **Acesso não transacionado de FILESTREAM**  
 Especifique uma das seguintes opções para acesso não transacional através do sistema de arquivos aos dados FILESTREAM armazenados em FileTables: **OFF**, **READ_ONLY**ou **FULL**. Se FILESTREAM não estiver habilitado no servidor, esse valor será definido como OFF e será desabilitado. Para obter mais informações, veja [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
## <a name="miscellaneous"></a>Diversos  
 **Padrão ANSI NULL**  
 Permita valores nulos para todos os tipos de dados ou colunas definidos pelo usuário que não estejam explicitamente definidos como `NOT NULL` durante uma instrução `CREATE TABLE` ou `ALTER TABLE` (o estado padrão). Para obter mais informações, veja [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql) e [SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql).  
  
 **ANSI NULLs habilitado**  
 Especifique o comportamento dos operadores de comparação Igual a (`=`) e Diferente de (`<>`) quando usados com valores nulos. Os valores possíveis `True` são (on) `False` e (off). Quando `True`, todas as comparações com um valor nulo são avaliadas como UNKNOWN. Quando `False`, as comparações de valores não-Unicode para um valor nulo `True` são avaliadas se ambos os valores forem nulos. Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).  
  
 **Preenchimento ANSI habilitado**  
 Especifique se preenchimento ANSI está ativado ou desativado. Os valores permitidos `True` são (on) `False` e (off). Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Avisos ANSI habilitados**  
 Especifique comportamento padrão ISO para várias condições de erro. Quando `True`, uma mensagem de aviso será gerada se valores nulos aparecerem em funções de agregação (como Sum, AVG, Max, min, Desv, DESVPADP, var, VARP ou Count). Quando `False`, nenhum aviso é emitido. Para obter mais informações, veja [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql).  
  
 **Anular aritmética habilitada**  
 Especifique se a opção de banco de dados de anulação de aritmética está habilitada ou não. Os valores possíveis são `True` e `False`. Quando `True`, um estouro ou erro de divisão por zero causa o encerramento da consulta ou lote. Se o erro ocorrer em uma transação, a transação será revertida. Quando `False`, uma mensagem de aviso será exibida, mas a consulta, lote ou transação continuará como se nenhum erro tivesse ocorrido. Para obter mais informações, veja [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql).  
  
 **Concatenar nulo produz nulo**  
 Especifique o comportamento quando valores nulos são concatenados. Quando o valor da propriedade `True`é `string` , + NULL retorna NULL. Quando `False`, o resultado é `string`. Para obter mais informações, veja [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql).  
  
 **Encadeamento de propriedades de bancos de dados habilitado**  
 Esse valor somente leitura indica se o encadeamento de propriedades de bancos de dados foi habilitado. Quando `True`, o banco de dados pode ser a origem ou o destino de uma cadeia de propriedade de banco de dados. Use a instrução ALTER DATABASE para definir essa propriedade.  
  
 **Otimização de correlação de data habilitada**  
 Quando `True`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o mantém as estatísticas de correlação entre as duas tabelas no banco de dados que são vinculadas por uma `datetime` restrição FOREIGN KEY e têm colunas.  
  
 Quando `False`, as estatísticas de correlação não são mantidas.  
  
 **Anular arredondamento numérico**  
 Especifique como o banco de dados trata erros de arredondamento. Os valores possíveis são `True` e `False`. Quando `True`, um erro é gerado quando ocorre perda de precisão em uma expressão. Quando `False`, as perdas de precisão não geram mensagens de erro e o resultado é arredondado para a precisão da coluna ou variável que armazena o resultado. Para obter mais informações, veja [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql).  
  
 **Parametrização**  
 Quando definidas como **SIMPLE**, as consultas são parametrizadas com base no comportamento padrão do banco de dados. Quando **forçada**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametriza todas as consultas no banco de dados.  
  
 **Identificadores entre aspas habilitados**  
 Especifique se palavras-chave do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser usadas como identificadores (um nome de variável ou objeto) se estiverem incluídas entre aspas. Os valores possíveis são `True` e `False`. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **Gatilhos recursivos habilitados**  
 Especifique se gatilhos podem ser acionados por outros gatilhos. Os valores possíveis são `True` e `False`. Quando definido como `True`, isso habilita o acionamento recursivo de gatilhos. Quando definido como `False`, somente a recursão direta é impedida. Para desabilitar a recursão indireta, defina a opção de servidor nested triggers como 0 usando sp_configure. Para obter mais informações, consulte [Criar gatilhos aninhados](../triggers/create-nested-triggers.md).  
  
 `Trustworthy`  
 Ao exibir `True`, essa opção somente leitura indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite o acesso a recursos fora do banco de dados sob um contexto de representação estabelecido no banco de dados. Contextos de representação podem ser estabelecidos dentro do banco de dados usando a instrução de usuário EXECUTE AS ou a cláusula EXECUTE AS em módulos do banco de dados.  
  
 Para ter acesso, o proprietário do banco de dados também precisa ter a permissão AUTHENTICATE SERVER no nível do servidor.  
  
 Essa propriedade também permite criação e execução de assemblies de acesso inseguros e externos dentro do banco de dados. Além disso, para configurar essa propriedade como `True`, o proprietário do banco de dados deve ter a permissão EXTERNAL ACCESS ASSEMBLY ou UNSAFE ASSEMBLY no nível do servidor.  
  
 Por padrão, todos os bancos de dados de usuário e todos os bancos de dados do sistema (com exceção do **msdb**) têm essa `False`propriedade definida como. O valor não pode ser alterado para os bancos de dados **modelo** e **tempdb** .  
  
 TRUSTWORTHY é definido como `False` sempre que um banco de dados está conectado ao servidor.  
  
 A abordagem recomendada para acessar recursos fora do banco de dados em um contexto de representação é usar certificados e assinaturas em vez da opção `Trustworthy`.  
  
 Para definir essa propriedade, use a instrução ALTER DATABASE.  
  
 **Formato de armazenamento VarDecimal Habilitado**  
 Essa opção é somente leitura a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versões posteriores, todos os bancos de dados são habilitados para o formato de armazenamento vardecimal. Essa opção usa [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
## <a name="recovery"></a>Recuperação  
 **Verificação de página**  
 Especifique a opção usada para descobrir e relatar transações de E/S incompletas provocadas por erros de E/S em disco. Os valores possíveis são **Nenhum**, **TornPageDetection**e **Soma de Verificação**. Para obter mais informações, veja [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
 **Tempo de recuperação de destino (segundos)**  
 Especifica o salto máximo no tempo, expresso em segundos, para recuperar o banco de dados especificado no caso de uma falha. Para obter mais informações, consulte [Pontos de verificação de banco de dados &#40;SQL Server&#41;](../logs/database-checkpoints-sql-server.md).  
  
## <a name="state"></a>Estado  
 **Banco de dados somente leitura**  
 Especifique se o banco de dados é somente leitura. Os valores possíveis são `True` e `False`. Quando `True`, os usuários só podem ler dados no banco de dados. Os usuários não podem modificar os dados ou objetos de banco de dados. No entanto, o próprio banco de dados pode ser excluído usando a instrução DROP DATABASE. O banco de dados não pode estar em uso quando um novo valor para a opção **Banco de Dados Somente Leitura** estiver especificado. O banco de dados mestre é a exceção e só o administrador do sistema pode usar o mestre enquanto a opção estiver sendo definida.  
  
 **Estado do banco de dados**  
 Exiba o estado atual do banco de dados. Ela não é editável. Para obter mais informações sobre o **Estado do Banco de Dados**, consulte [Database States](database-states.md)  
  
 **Acesso restrito**  
 Especifique quais usuários podem acessar o banco de dados. Os valores possíveis são:  
  
-   **Vários**  
  
     O estado normal de um banco de dados de produção. Permite que vários usuários acessem o banco de dados de uma vez.  
  
-   **Exclusivo**  
  
     Usado para ações de manutenção, apenas um usuário tem permissão para acessar o banco de dados por vez.  
  
-   **Restricted (Restrito)**  
  
     Apenas membros das funções db_owner, dbcreator ou sysadmin podem usar o banco de dados.  
  
 **Criptografia habilitada**  
 Quando `True`, esse banco de dados é habilitado para criptografia de banco de dados. Uma Chave de Criptografia do Banco de Dados é necessária para criptografia. Para obter mais informações, veja [TDE &#40;Transparent Data Encryption&#41;](../security/encryption/transparent-data-encryption.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
