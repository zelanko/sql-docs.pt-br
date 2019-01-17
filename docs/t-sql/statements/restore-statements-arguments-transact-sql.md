---
title: Argumentos de RESTORE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- RESTORE statement, arguments
- RESTORE statement
ms.assetid: 4bfe5734-3003-4165-afd4-b1131ea26e2b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 78dfe43617d9a519b479e53abbabcf311d726b1d
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980512"
---
# <a name="restore-statements---arguments-transact-sql"></a>Instruções RESTORE – argumentos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Este tópico documenta os argumentos descritos nas seções de Sintaxe da instrução RESTORE {DATABASE|LOG} e do conjunto associado de instruções auxiliares: RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY e RESTORE VERIFYONLY. Há suporte para a maioria dos argumentos apenas por um subconjunto dessas seis instruções. O suporte a cada argumento é indicado na descrição do argumento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
 Para obter a sintaxe, consulte os seguintes tópicos:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="arguments"></a>Argumentos  
 DATABASE  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica o banco de dados de destino. Se uma lista de arquivos e grupos de arquivos estiver especificada, apenas esses arquivos e grupos de arquivos serão restaurados.  
  
 Para um banco de dados que usa o modelo de recuperação completa ou bulk-logged, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que se faça backup do final do log antes da restauração do banco de dados. Restaurar um banco de dados sem antes fazer backup do final do log resultará em um erro, a não ser que a instrução RESTORE DATABASE contenha a cláusula WITH REPLACE ou WITH STOPAT, que deve especificar um momento ou transação que ocorreu após o final do backup de dados. Para obter mais informações sobre backups da parte final do log, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 LOG  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica que um backup do log de transações será aplicado a este banco de dados. Os logs de transação devem ser aplicados em ordem sequencial. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica o log de transações com backup para garantir que as transações estão sendo carregadas no banco de dados correto e na sequência correta. Para aplicar vários logs de transações, use a opção NORECOVERY em todas as operações de restauração exceto na última.  
  
> [!NOTE]  
>  Normalmente, o último log restaurado é o backup do final do log. Um *backup da parte final do log* é um backup de log feito exatamente antes da restauração de um banco de dados, normalmente após uma falha do banco de dados. Fazer um backup do final do log do banco de dados que está possivelmente danificado evita perda de trabalho capturando o log que ainda não tem backup (o final do log). Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
 { _database\_name_ | **@**_database\_name\_var_}  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 É o banco de dados no qual o log ou banco de dados completo é restaurado. Se for fornecido como uma variável (**@**_database\_name\_var_), esse nome poderá ser especificado como uma constante de cadeia de caracteres (**@**_database\_name\_var_ = *database*\_*name*) ou como uma variável de tipo de dados string, exceto para os tipos de dados **ntext** ou **text**.  
  
 \<file_or_filegroup_or_page> [ **,**...*n* ]  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica o nome de uma página, grupo de arquivos ou arquivo lógico a ser incluído em uma instrução RESTORE DATABASE ou RESTORE LOG. É possível especificar uma lista de arquivos ou grupos de arquivos.  
  
 Para um banco de dados que usa o modelo de recuperação simples, as opções FILE e FILEGROUP serão permitidas apenas se os arquivos de destino ou grupos de arquivos forem somente leitura ou se esta for uma restauração PARTIAL (que resulta em um [grupo de arquivos extinto](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)).  
  
 Para um banco de dados que usa o modelo de recuperação completa ou bulk-logged, após usar RESTORE DATABASE para restaurar um ou mais arquivos, e/ou páginas, normalmente você deve aplicar o log de transações nos arquivos que contêm os dados restaurados. A aplicação do log torna esses arquivos consistentes com o restante do banco de dados. As exceções são as seguintes:  
  
-   Se os arquivos que estão sendo restaurados eram somente leitura antes do último backup feito, um log de transações não precisará ser aplicado e a instrução RESTORE informará sobre essa situação.  
  
-   Se o backup contiver o grupo de arquivos primário e uma restauração parcial estiver sendo executada. Nesse caso, o log de restauração não é necessário porque o log é restaurado automaticamente do conjunto de backup.  
  
FILE **=** { *logical_file_name_in_backup*| **@**_logical\_file\_name\_in\_backup\_var_}  
 Nomeia um arquivo a ser incluído na restauração do banco de dados.  
  
FILEGROUP **=** { *logical_filegroup_name* | **@**_logical\_filegroup\_name\_var_ }  
 Nomeia um grupo de arquivos a ser incluído na restauração do banco de dados.  
  
 **Observação** FILEGROUP é permitido no modelo de recuperação simples apenas se o grupo de arquivos especificado é somente leitura e esta é uma restauração parcial (ou seja, se WITH PARTIAL é usado). Todos os grupos de arquivos de leitura/gravação não restaurados são marcados como expirados e não podem ser restaurados subsequentemente no banco de dados resultante.  
  
READ_WRITE_FILEGROUPS  
 Seleciona todos os grupos de arquivos de leitura/gravação. Essa opção é útil principalmente quando você tem vários grupos de arquivos somente leitura que deseja restaurar após os grupos de arquivos de leitura/gravação.  
  
PAGE = **'**_file_**:**_page* [ **,**...*n* ]**'**  
 Especifica uma lista de uma ou mais páginas para uma restauração de página (o que tem suporte apenas para bancos de dados que usam os modelos de recuperação completa ou bulk-logged). Os valores são os seguintes:  
  
PAGE  
 Indica uma lista de um ou mais arquivos e páginas.  
  
 *file*  
 É a ID do arquivo que contém uma página específica a ser restaurada.  
  
 *page*  
 É a ID da página a ser restaurada no arquivo.  
  
 *n*  
 É um espaço reservado que indica que várias páginas podem ser especificadas.  
  
 O número máximo de páginas que podem ser restauradas em um único arquivo em uma sequência de restauração é 1000. No entanto, se houver mais que um pequeno número de páginas danificadas em um arquivo, considere restaurar o arquivo inteiro em vez das páginas.  
  
> [!NOTE]  
>  Restaurações de páginas nunca são recuperadas.  
  
 Para obter mais informações sobre restauração de página, consulte [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md).  
  
 [ **,**...*n* ]  
 É um espaço reservado que indica que vários arquivos, grupos de arquivos e páginas podem ser especificados em uma lista separada por vírgulas. O número é ilimitado.  
  
FROM { \<backup_device> [ **,**...*n* ]| \<database_snapshot> } Normalmente, especifica os dispositivos de backup do qual restaurar o backup. Como alternativa, em uma instrução RESTORE DATABASE, a cláusula FROM pode especificar o nome de um instantâneo do banco de dados para o qual você está revertendo o banco de dados e, nesse caso, nenhuma cláusula WITH é permitida.  
  
 Se a cláusula FROM for omitida, a restauração de um backup não ocorrerá. Em vez disso, o banco de dados é recuperado. Isso permite recuperar um banco de dados que foi restaurado com a opção NORECOVERY ou reverter para um servidor em espera. Se a cláusula FROM for omitida, NORECOVERY, RECOVERY ou STANDBY devem ser especificados na cláusula WITH.  
  
 \<backup_device> [ **,**...*n* ] Especifica os dispositivos de backup lógicos ou físicos a serem usados para a operação de restauração.  
  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 \<backup_device>::= Especifica um dispositivo de backup lógico ou físico a ser usado para a operação de backup, da seguinte maneira:  
  
 { _logical\_backup\_device\_name_ | **@**_logical\_backup\_device\_name\_var_ }  
 É o nome lógico que deve seguir as regras de identificadores dos dispositivos de backup criados por **sp_addumpdevice** dos quais o banco de dados é restaurado. Se for fornecido como uma variável (**@**_logical\_backup\_device\_name\_var_), o nome do dispositivo de backup poderá ser especificado como uma constante de cadeia de caracteres (**@**_logical\_backup\_device\_name\_var_ = _logical\_backup\_device\_name_) ou como uma variável do tipo de dados string, exceto os tipos de dados **ntext** ou **text**.  
  
 {DISK | TAPE } **=** { **'**_physical\_backup\_device\_name_**'** | **@**_physical\_backup\_device\_name\_var_ }  
 Permite restaurar backups do disco nomeado ou dispositivo de fita. Os tipos de dispositivo de disco e fita devem ser especificados com o nome real (por exemplo, caminho completo e nome de arquivo) do dispositivo: `DISK ='Z:\SQLServerBackups\AdventureWorks.bak'` ou `TAPE ='\\\\.\TAPE0'`. Se for especificado como uma variável (**@**_physical\_backup\_device\_name\_var_), o nome do dispositivo poderá ser especificado como uma constante de cadeia de caracteres (**@**_physical\_backup\_device\_name\_var_ = '*physcial_backup_device_name*') ou como uma variável do tipo de dados String, exceto para os tipos de dados **ntext** ou **text**.  
  
 Se usando um servidor de rede com um nome de UNC (que deve conter o nome de máquina), especifique um tipo de dispositivo de disco. Para obter informações sobre como usar nomes UNC, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 A conta sob a qual você está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter acesso READ ao computador remoto ou servidor de rede para executar uma operação RESTORE.  
  
 *n*  
 É um espaço reservado que indica que até 64 dispositivos de backup podem ser especificados em uma lista separada por vírgula.  
  
 Se uma sequência de restauração precisar de tantos dispositivos de backup quantos foram usados para criar o conjunto de mídias ao qual o backup pertence, dependerá de se a restauração é offline ou online, da seguinte maneira:  
  
-   A restauração off-line permite que um backup seja restaurado usando menos dispositivos que os usados para criar o backup.  
  
-   A restauração on-line requer todos os dispositivos de backup. Uma tentativa de restaurar com menos dispositivos falhará.  
  
 Por exemplo, considere um caso em que o backup de um banco de dados foi feito para quatro unidades de fita conectadas ao servidor. Uma restauração online requer que você tenha quatro unidades conectadas ao servidor. Uma restauração offline permite restaurar o backup se houver menos de quatro unidades na máquina.  
  
> [!NOTE]  
>  Ao restaurar um backup de um conjunto de mídias espelhado, você pode especificar apenas um único espelho para cada família de mídia. Porém, na presença de erros, a existência de outros espelhos permite que alguns problemas de restauração sejam resolvidos rapidamente. Você pode substituir um volume de mídia danificado pelo volume correspondente de outro espelho. Lembre-se de que, para restaurações offline, é possível restaurar a partir de menos dispositivos do que as famílias de mídia, mas cada família é processada apenas uma vez.  
  
\<database_snapshot>::=  
**Com suporte de:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
DATABASE_SNAPSHOT **=**_database\_snapshot\_name_  
 Reverte o banco de dados no instantâneo do banco de dados especificado por *database_snapshot_name*. A opção DATABASE_SNAPSHOT está disponível apenas para uma restauração completa do banco de dados. Em uma operação de reversão, o instantâneo do banco de dados ocupa o lugar de um backup completo do banco de dados.  
  
 Uma operação de reversão requer que o instantâneo do banco de dados especificado seja o único no banco de dados. Durante a operação de reversão, o instantâneo e o banco de dados de origem são marcados como `In restore`. Para obter mais informações, consulte a seção "Comentários" em [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
### <a name="with-options"></a>Opções WITH  
 Especifica as opções a serem usadas por uma operação de restauração. Para obter um resumo de quais instruções usam cada opção, consulte "Resumo de suporte para opções WITH" mais adiante neste tópico.  
  
> [!NOTE]  
>  As opções WITH são organizadas aqui na mesma ordem que na seção "Sintaxe" em [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 PARTIAL  
 **Com suporte de:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica uma operação de restauração parcial que restaura o grupo de arquivos primário e qualquer grupo de arquivos secundário especificado. A opção PARCIAL seleciona o grupo de arquivos primário implicitamente. Não é necessário especificar FILEGROUP = 'PRIMARY'. Para restaurar um grupo de arquivos secundário, você deve especificar o grupo de arquivos usando a opção FILE ou a opção FILEGROUP explicitamente.  
  
 A opção PARTIAL não é permitida em instruções RESTORE LOG.  
  
 A opção PARTIAL inicia o estágio inicial de uma restauração por etapas, o que permite que os grupos de arquivos restantes sejam restaurados posteriormente. Para obter mais informações, veja [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).  
  
 [ **RECOVERY** | NORECOVERY | STANDBY ]  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **RECOVERY**  
 Instrui a operação de restauração a reverter todas as transações não confirmadas. Após o processo de recuperação, o banco de dados está pronto para uso. Se NORECOVERY, RECOVERY ou STANDBY não estiverem especificados, RECOVERY será o padrão.  
  
 Se operações subsequentes de RESTORE (RESTORE LOG ou RESTORE DATABASE de diferencial) forem planejadas, NORECOVERY ou STANDBY deverão ser especificadas no lugar.  
  
 Ao restaurar conjuntos de backup de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], uma atualização do banco de dados pode ser necessária. Essa atualização é executada automaticamente quando WITH RECOVERY é especificado. Para obter mais informações, veja [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
> [!NOTE]  
>  Se a cláusula FROM for omitida, NORECOVERY, RECOVERY ou STANDBY devem ser especificados na cláusula WITH.  
  
 NORECOVERY  
 Instrui a operação de restauração a não reverter nenhuma transação não confirmada. Se outro log de transações precisar ser aplicado posteriormente, especifique a opção NORECOVERY ou STANDBY. Se NORECOVERY, RECOVERY ou STANDBY não estiverem especificados, RECOVERY será o padrão. Durante uma operação de restauração offline usando a opção NORECOVERY, o banco de dados não será utilizável.  
  
 Para restaurar um backup do banco de dados e um ou mais logs de transações ou sempre que várias instruções RESTORE forem necessárias (por exemplo, ao restaurar um backup completo seguido por um backup diferencial do banco de dados), RESTORE requer a opção WITH NORECOVERY em todas as instruções, menos na RESTORE final. A prática recomendada é usar WITH NORECOVERY em TODAS as instruções em uma sequência de restauração de várias etapas até que o ponto de recuperação desejado seja atingido e, em seguida, usar uma instrução RESTORE WITH RECOVERY separada apenas para recuperação.  
  
 Quando usado com uma operação de restauração de arquivos ou de grupos de arquivos, NORECOVERY força o banco de dados a permanecer no estado de restauração após a operação de restauração. Isto é útil em qualquer um destas situações:  
  
-   Um script de restauração está sendo executado e o log sempre está sendo aplicado.  
  
-   Uma sequência de restaurações de arquivos é usada e o banco de dados não tem o objetivo de ser utilizável entre duas das operações de restauração.  
  
 Em alguns casos RESTORE WITH NORECOVERY efetua o conjunto de roll-forward com avanço suficiente para ficar consistente com o banco de dados. Nesses casos, a reversão não ocorre e os dados permanecem offline, como é esperado com essa opção. No entanto, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] emite uma mensagem informando que o conjunto de roll-forward pode ser recuperado agora usando a opção RECOVERY.  
  
STANDBY **=**_standby\_file\_name_  
 Especifica um arquivo em espera que permite que os efeitos da recuperação sejam desfeitos. A opção STANDBY é permitida para restauração offline (incluindo restauração parcial). A opção não é permitida para restauração online. Tentar especificar a opção STANDBY para uma operação de restauração online faz com que a operação de restauração falhe. STANDBY também não é permitido quando uma atualização de banco de dados é necessária.  
  
 O arquivo em espera é usado para manter uma pré-imagem de "copy-on-write" durante a fase de desfazer um RESTORE WITH STANDBY. O arquivo em espera permite que um banco de dados seja aberto para acesso somente leitura entre restaurações do log de transações e possa ser usado com situações de servidor em espera passiva ou em situações especiais de recuperação, nas quais é útil inspecionar o banco de dados entre restaurações do log. Após uma operação RESTORE WITH STANDBY, o arquivo de desfazer é excluído automaticamente pela próxima operação RESTORE. Se esse arquivo em espera for excluído manualmente antes da próxima operação RESTORE, o banco de dados inteiro deverá ser restaurado novamente. Enquanto o banco de dados está em estado STANDBY, você deve tratar esse arquivo em espera com o mesmo cuidado como com qualquer outro arquivo do banco de dados. Ao contrário de outros arquivos do banco de dados, esse arquivo é mantido aberto pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] apenas durante operações de restauração ativas.  
  
 O *standby_file_name* especifica um arquivo em espera cujo local é armazenado no log do banco de dados. Se um arquivo existente estiver usando o nome especificado, o arquivo será substituído. Caso contrário, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criará o arquivo.  
  
 O requisito de tamanho de um determinado arquivo em espera depende do volume de ações de desfazer resultantes das transações não confirmadas durante a operação de restauração.  
  
> [!IMPORTANT]  
>  Se o espaço em disco disponível se esgotar na unidade que contém o nome do arquivo em espera especificado, a operação de restauração será parada.  
  
 Para obter uma comparação de RECOVERY e NORECOVERY, consulte a seção "Comentários" em [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
LOADHISTORY  
 **Com suporte de:**  [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Especifica que a operação de restauração carrega as informações nas tabelas de histórico do **msdb**. A opção LOADHISTORY carrega informações, do único conjunto de backup que está sendo verificado, sobre backups do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenados no conjunto de mídias nas tabelas do histórico de backup e restauração no banco de dados **msdb**. Para obter mais informações sobre tabelas de histórico, consulte [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md).  
  
#### <a name="generalwithoptions--n-"></a>\<general_WITH_options> [ ,...n ]  
 Todas as opções gerais de WITH têm suporte nas instruções RESTORE DATABASE e RESTORE LOG. Algumas dessas opções também são compatíveis com uma ou mais instruções auxiliares, conforme indicado abaixo.  
  
##### <a name="restore-operation-options"></a>Opções da operação de restauração  
 Essas opções afetam o comportamento da operação de restauração.  
  
MOVE **'**_logical\_file\_name\_in\_backup_**'** TO **'**_operating\_system\_file\_name_**'** [ ...*n* ]  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Especifica que o arquivo de dados ou de log cujo nome lógico é especificado por *logical_file_name_in_backup* deve ser movido com sua restauração no local especificado por *operating_system_file_name*. O nome do arquivo lógico de um arquivo de log ou de dados em um conjunto de backup corresponde ao seu nome lógico no banco de dados quando o conjunto de backup foi criado.  
  
*n* é um espaço reservado que indica que você pode especificar instruções MOVE adicionais. Especifique uma instrução MOVE para cada arquivo lógico que você deseja restaurar do conjunto de backup para um novo local. Por padrão, o arquivo *logical_file_name_in_backup* é restaurado em seu local original.  
  
> [!NOTE]  
>  Para obter uma lista dos arquivos lógicos do conjunto de backup, use RESTORE FILELISTONLY.  
  
 Se uma instrução RESTORE for usada para relocar um banco de dados no mesmo servidor ou copiá-lo para um servidor diferente, a opção MOVE poderá ser necessária para relocar os arquivos do banco de dados e para evitar colisões com os arquivos existentes.  
  
 Quando usada com RESTORE LOG, a opção MOVE pode ser usada apenas para relocar arquivos que foram adicionados durante o intervalo coberto pelo log que está sendo restaurado. Por exemplo, se o backup do log contiver uma operação de adição de arquivo para o arquivo `file23`, esse arquivo poderá ser relocado usando a opção MOVE em RESTORE LOG.  
  
 Quando usada com o Backup de Instantâneo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção MOVE pode ser usada somente para relocar arquivos em um blob do Azure na mesma conta de armazenamento do blob original. A opção MOVE não pode ser usada para restaurar o backup de instantâneo em um arquivo local ou em outra conta de armazenamento.  
  
 Se uma instrução RESTORE VERIFYONLY for usada quando você planejar relocar um banco de dados no mesmo servidor ou copiá-lo para um servidor diferente, a opção MOVE poderá ser necessária para verificar se há espaço suficiente disponível no destino e para identificar potenciais colisões com arquivos existentes.  
  
 Para obter mais informações, veja [Copiar bancos de dados com Backup e Restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md).  
  
CREDENTIAL  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
**Aplica-se ao**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Usado apenas ao restaurar um backup do serviço de Armazenamento de Blobs do Microsoft Azure.  
  
> [!NOTE]  
>  Com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 até o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode apenas restaurar de um único dispositivo ao fazer uma restauração de uma URL. Para fazer uma restauração de vários dispositivos ao restaurar de uma URL, é necessário usar o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)) e usar os tokens SAS (Assinatura de Acesso Compartilhado). Para obter mais informações, consulte [Habilitar o backup gerenciado do SQL Server no Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) e [Simplificando a criação de credenciais do SQL com tokens SAS (Assinatura de Acesso Compartilhado) no Armazenamento do Azure com o PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
 REPLACE  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve criar o banco de dados especificado e seus arquivos relacionados, mesmo que já exista outro banco de dados com o mesmo nome. Nesse caso, o banco de dados existente é excluído. Quando a opção REPLACE não é especificada, ocorre uma verificação de segurança. Isto impede que um banco de dados diferente seja substituído por acidente. A verificação de segurança garante que a instrução RESTORE DATABASE não restaurará o banco de dados no servidor atual, se existirem as seguintes condições:  
  
-   O banco de dados nomeado na instrução RESTORE já existe no servidor atual, e  
  
-   O nome do banco de dados é diferente do nome de banco de dados registrado no conjunto de backup.  
  
 REPLACE também permite que RESTORE substitua um arquivo existente que não pode ser verificado como pertencente ao banco de dados que está sendo restaurado. Normalmente, RESTORE se recusa a substituir arquivos preexistentes. WITH REPLACE também pode ser usado da mesma maneira para a opção RESTORE LOG.  
  
 REPLACE também substitui o requisito de fazer backup do log final antes da restauração do banco de dados.  
  
 Para obter mais informações sobre o impacto do uso da opção REPLACE, consulte [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
RESTART  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve reinicializar uma operação de restauração que foi interrompida. RESTART reinicia a operação de restauração no ponto em que foi interrompida.  
  
RESTRICTED_USER  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Restringe o acesso para o banco de dados recém-restaurado a membros das funções **db_owner**, **dbcreator** ou **sysadmin**.  RESTRICTED_USER substitui a opção DBO_ONLY. DBO_ONLY foi descontinuado com [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Use com a opção RECOVERY.  
  
##### <a name="backup-set-options"></a>Opções de conjunto de backup  
 Essas opções funcionam no conjunto de backup que contém o backup a ser restaurado.  
  
FILE **=**{ *backup_set_file_number* | **@**_backup\_set\_file\_number_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Identifica o conjunto de backup a ser restaurado. Por exemplo, um *backup_set_file_number* de **1** indica o primeiro conjunto de backup na mídia de backup e um *backup_set_file_number* de **2** indica o segundo conjunto de backup. Você pode obter o *backup_set_file_number* de um backup definido usando a instrução [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) .  
  
 Quando não especificado, o padrão é **1**, com exceção de RESTORE HEADERONLY, em que todos os conjuntos de backup no conjunto de mídias são processados. Para obter mais informações, consulte "Especificando um conjunto de backup", mais adiante neste tópico.  
  
> [!IMPORTANT]  
>  Essa opção FILE não está relacionada à opção FILE para especificar um arquivo de banco de dados, FILE **=** { *logical_file_name_in_backup* | **@**_logical\_file\_name\_in\_backup\_var_ }.  
  
 PASSWORD  **=** { *password* | **@**_password\_variable_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Fornece a senha do conjunto de backup. A senha de um conjunto de backup é uma cadeia de caracteres.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Se uma senha foi especificada quando o conjunto de backup foi criado, essa senha será necessária para executar qualquer operação de restauração do conjunto de backup. É um erro para especificar a senha incorreta ou para especificar uma senha se o conjunto de backup não tiver uma.  
  
> [!IMPORTANT]  
>  Essa senha fornece apenas uma proteção fraca para o conjunto de mídias. Para obter mais informações, consulte a seção Permissões da instrução relevante.  
  
##### <a name="media-set-options"></a>Opções de conjunto de mídias  
 Essas opções funcionam no conjunto de mídias como um todo.  
  
 MEDIANAME **=** { *media_name* | **@**_media\_name\_variable_}  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Especifica o nome da mídia. Se fornecido, o nome da mídia deve corresponder ao nome da mídia nos volumes de backup. Caso contrário, a operação de restauração será finalizada. Se nenhum nome de mídia for fornecido na instrução RESTORE, a verificação de um nome de mídia correspondente nos volumes de backup não será executada.  
  
> [!IMPORTANT]  
>  O uso consistente de nomes de mídia em operações de backup e restauração fornece uma verificação extra de segurança para a mídia selecionada para a operação de restauração.  
  
 MEDIAPASSWORD **=** { *mediapassword* | **@**_mediapassword\_variable_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Fornece a senha do conjunto de mídias. A senha de um conjunto de mídias é uma cadeia de caracteres.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Se uma senha foi fornecida quando o conjunto de mídias foi formatado, essa senha será necessária para acessar qualquer conjunto de backup no conjunto de mídias. É um erro para especificar a senha incorreta ou para especificar uma senha se o conjunto de mídias não tiver uma.  
  
> [!IMPORTANT]  
>  Essa senha fornece apenas uma proteção fraca para o conjunto de mídias. Para obter mais informações, consulte a seção "Permissões" da instrução relevante.  
  
 BLOCKSIZE **=** { *blocksize* | **@**_blocksize\_variable_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica o tamanho do bloco físico, em bytes. Os tamanhos com suporte são 512, 1024, 2048, 4096, 8192, 16384, 32768 e 65536 (64 KB) bytes. O padrão é 65536 para dispositivos de fita e 512 para outros dispositivos. Normalmente, essa opção é desnecessária porque RESTORE seleciona automaticamente um tamanho de bloco apropriado ao dispositivo. A declaração explícita de um tamanho de bloco substitui a seleção automática de tamanho de bloco.  
  
 Se estiver restaurando um backup de um CD-ROM, especifique BLOCKSIZE=2048.  
  
> [!NOTE]  
>  Normalmente, essa opção afeta o desempenho apenas durante a leitura de dispositivos de fita.  
  
##### <a name="data-transfer-options"></a>Opções de transferência de dados  
 As opções permitem otimizar a transferência de dados do dispositivo de backup.  
  
 BUFFERCOUNT **=** { *buffercount* | **@**_buffercount\_variable_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica o número total de buffers de E/S a ser usado para a operação de restauração. É possível especificar qualquer inteiro positivo. No entanto, grandes números de buffers podem provocar erros de "memória insuficiente" devido a espaço de endereço virtual inadequado no processo Sqlservr.exe.  
  
 O espaço total usado pelos buffers é determinado por: _buffercount_**\**_maxtransfersize_.  
  
 MAXTRANSFERSIZE **=** { _maxtransfersize_ | **@**_maxtransfersize\_variable_ }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 Especifica a maior unidade de transferência em bytes a ser usada entre a mídia de backup e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os valores possíveis são múltiplos de 65536 bytes (64 KB), estendendo-se até 4194304 bytes (4 MB).  
> [!NOTE]  
>  Quando o banco de dados tiver configurado o FILESTREAM ou incluir Grupos de Arquivos OLTP In-Memory, `MAXTRANSFERSIZE`, no momento da restauração deve ser maior ou igual ao que foi usado quando o backup foi criado.  
  
##### <a name="error-management-options"></a>Opções de gerenciamento de erros  
 Essas opções permitem determinar se somas de verificação de backup estão habilitadas para a operação de restauração e se a operação será interrompida quando um erro for encontrado.    
  
 { CHECKSUM | NO_CHECKSUM }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 O comportamento padrão é verificar somas de verificação se elas estiverem presentes e continuar sem verificação se não estiverem presentes.  
  
 CHECKSUM  
 Especifica que as somas de verificação de backup devem ser verificadas e, se o backup não tiver somas de verificação, faz com que a operação de restauração falhe com uma mensagem indicando que somas de verificação não estão presentes.  
  
> [!NOTE]  
>  As somas de verificação de página serão relevantes para operações de backup somente se as somas de verificação de backup forem usadas.  
  
 Por padrão, ao encontrar uma soma de verificação inválida, RESTORE relata um erro de soma de verificação e para. No entanto, se você especificar CONTINUE_AFTER_ERROR, a operação RESTORE continuará após retornar um erro de soma de verificação e o número da página que contém a soma de verificação inválida, se o dano permitir.  
  
 Para obter mais informações sobre como trabalhar com somas de verificação de backup, consulte [Possíveis erros de mídia durante backup e restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
 NO_CHECKSUM  
 Desabilita explicitamente a validação de somas de verificação pela operação de restauração.  
  
 { **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 STOP_ON_ERROR  
 Especifica que a operação de restauração para com o primeiro erro encontrado. Esse é o comportamento padrão para RESTORE, com exceção de VERIFYONLY que tem CONTINUE_AFTER_ERROR como o padrão.  
  
 CONTINUE_AFTER_ERROR  
 Determina que a operação de restauração deve continuar depois que um erro for encontrado.  
  
 Se um backup contiver páginas danificadas, será melhor repetir a operação de restauração usando um backup alternativo que não contenha os erros, por exemplo, um backup feito antes das páginas serem danificadas. No entanto, como um último recurso, é possível restaurar um backup danificado com o uso da opção CONTINUE_AFTER_ERROR da instrução RESTORE e tentar salvar os dados.  
  
##### <a name="filestream-options"></a>Opções de FILESTREAM  
 FILESTREAM ( DIRECTORY_NAME =*directory_name* )  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Um nome de diretório compatível com o Windows. Esse nome deve ser exclusivo entre todos os nomes de diretórios FILESTREAM no nível de banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A comparação de exclusividade é feita sem diferenciar maiúsculas de minúsculas, independentemente das configurações de ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### <a name="monitoring-options"></a>Opções de monitoramento  
 Essas opções permitem monitorar a transferência de dados do dispositivo de backup.  
  
 STATS [ **=** *percentage* ]  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 Exibe uma mensagem a cada vez que outra porcentagem for concluída e é usada para medir o progresso. Se *percentage* for omitido, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibirá uma mensagem após a conclusão de cada 10% (aproximadamente).  
  
 A opção STATS informa a porcentagem concluída de acordo com o limite de relatório do próximo intervalo. Esse limite é aproximadamente a porcentagem especificada. Por exemplo, com STATS=10, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] relata aproximadamente nesse intervalo. Por exemplo, em vez de exibir precisamente 40%, a opção pode exibir 43%. Para conjuntos de backup grandes, isso não é um problema porque a porcentagem concluída muda muito lentamente entre chamadas de E/S concluídas.  
  
##### <a name="tape-options"></a>Opções de fita  
 Essas opções são usadas apenas para dispositivos TAPE. Se um dispositivo que não seja de fita estiver sendo usado, essas opções serão ignoradas.  
  
 { **REWIND** | NOREWIND }  
 Essas opções são usadas apenas para dispositivos TAPE. Se um dispositivo não fita estiver sendo usado, essas opções serão ignoradas.  
  
 REWIND  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libera e rebobina a fita. REWIND é o padrão.  
  
 NOREWIND  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
 A especificação de NOREWIND em qualquer outra restauração gera um erro.  
  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém a fita aberta após a operação de backup. É possível usar essa opção para melhorar o desempenho ao executar várias operações de backup em uma fita.  
  
 NOREWIND implica em NOUNLOAD e essas opções são incompatíveis dentro de uma única instrução RESTORE.  
  
> [!NOTE]  
>  Se NOREWIND for usado, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reterá a propriedade da unidade de fita até que uma instrução BACKUP ou RESTORE em execução no mesmo processo use a opção REWIND ou UNLOAD ou que a instância do servidor seja encerrada. Manter a fita aberta evita que outros processos a acessem. Para obter informações sobre como exibir uma lista de fitas abertas e fechar uma fita aberta, consulte [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
 { **UNLOAD** | NOUNLOAD }  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md), [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md), [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md), [RESTORE REWINDONLY](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md) e [RESTORE VERIFYONLY](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
 Essas opções são usadas apenas para dispositivos TAPE. Se um dispositivo não fita estiver sendo usado, essas opções serão ignoradas.  
  
> [!NOTE]  
>  UNLOAD/NOUNLOAD é uma configuração de sessão que persiste durante a vida útil da sessão ou até que ela seja redefinida especificando a alternativa.  
  
 UNLOAD  
 Especifica que a fita é rebobinada e descarregada automaticamente quando o backup for concluído. UNLOAD é o padrão quando uma sessão começa.  
  
 NOUNLOAD  
 Especifica que depois da operação RESTORE, a fita permanece carregada na unidade de fita.  
  
#### <a name="replicationwithoption"></a><replication_WITH_option>  
 Esta opção será relevante somente se o banco de dados foi replicado quando o backup foi criado.  
  
 KEEP_REPLICATION  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
Use KEEP_REPLICATION ao configurar a replicação para trabalhar com envio de logs. Ela impede que as configurações de replicação sejam removidas quando um backup de banco de dados ou de log é restaurado em um servidor em espera passiva e o banco de dados é recuperado. Não é permitido especificar essa opção ao restaurar um backup com a opção NORECOVERY. Para garantir funções de replicação corretamente após a restauração:  
  
-   Os bancos de dados **msdb** e **mestre** no servidor em espera passiva devem estar sincronizados com os bancos de dados **msdb** e **mestre** no servidor primário.  
  
-   O servidor em espera passiva deve ser renomeado para usar o mesmo nome que o servidor primário.  
  
#### <a name="changedatacapturewithoption"></a><change_data_capture_WITH_option>  
 Essa opção será relevante apenas se o banco de dados estiver habilitado para Change Data Capture quando o backup foi criado.  
  
 KEEP_CDC  
 **Com suporte de:**  [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 KEEP_CDC deve ser usado para impedir que as configurações de captura de dados de alterações sejam removidas quando um backup de banco de dados ou de log é restaurado em outro servidor e o banco de dados é recuperado. Não é permitido especificar essa opção ao restaurar um backup com a opção NORECOVERY.  
  
 A restauração do banco de dados com KEEP_CDC não cria os trabalhos de 	captura de dados de alterações. Para extrair alterações do log após restaurar o banco de dados, recrie o trabalho do processo de captura e o trabalho de limpeza do banco de dados restaurado. Para obter informações, consulte [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).  
  
 Para obter informações sobre como usar a captura de dados de alterações com o espelhamento de banco de dados, consulte [Change Data Capture e outros recursos do SQL Server](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md).  
  
#### <a name="servicebrokerwithoptions"></a>\<service_broker_WITH_options>  
 Ativa ou desativa a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] ou define um novo identificador do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Essa opção será relevante apenas se o [!INCLUDE[ssSB](../../includes/sssb-md.md)] estava habilitado (ativado) para o banco de dados quando o backup foi criado.  
  
 { ENABLE_BROKER | ERROR_BROKER_CONVERSATIONS | NEW_BROKER }  
 **Com suporte de:**  [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 ENABLE_BROKER  
 Especifica que a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é habilitada no final da restauração para que as mensagens possam ser enviadas imediatamente. Por padrão, a entrega de mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)] é desabilitado durante a restauração. O banco de dados retém o identificador do Service Broker.  
  
 ERROR_BROKER_CONVERSATIONS  
 Encerra todas as conversas com um erro que declara que o banco de dados está anexado ou restaurado. Isso permite que seus aplicativos executem a limpeza habitual para conversas existentes. A entrega de mensagens do Service Broker permanece desabilitada até que essa operação seja concluída e, em seguida, é habilitada. O banco de dados retém o identificador do Service Broker.  
  
 NEW_BROKER  
 Especifica que o banco de dados seja atribuído a um novo identificador do Service Broker. Como o banco de dados é considerado um novo Service Broker, as conversas existentes nele são imediatamente removidas sem produzir mensagens de caixa de diálogo de término. Qualquer rota que referencia o antigo identificador do Service Broker deverá ser recriada com o novo identificador.  
  
#### <a name="pointintimewithoptions"></a>\<point_in_time_WITH_options>  
 **Com suporte de:**  [RESTORE {DATABASE|LOG}](../../t-sql/statements/restore-statements-transact-sql.md) e apenas para os modelos de recuperação bulk-logged ou completa.  
  
 Você pode restaurar um banco de dados para uma transação ou momento específico, especificando o ponto de recuperação de destino em uma cláusula STOPAT, STOPATMARK ou STOPBEFOREMARK. Uma transação ou momento especificado sempre é restaurado a partir de um backup de log. Em cada instrução RESTORE LOG da sequência de restauração, você deve especificar a transação ou o tempo de destino em uma cláusula STOPAT, STOPATMARK ou STOPBEFOREMARK idêntica.  
  
 Como um pré-requisito para uma restauração pontual, você deve restaurar primeiro um backup de banco de dados completo cujo ponto de extremidade seja anterior ao ponto de recuperação de destino. Para ajudar a identificar qual backup de banco de dados restaurar, opcionalmente, você pode especificar a cláusula WITH STOPAT, STOPATMARK ou STOPBEFOREMARK em uma instrução RESTORE DATABASE para gerar um erro, se um backup de dados for muito recente para o tempo de destino especificado. Mas o backup de dados completo é sempre restaurado, mesmo que ele contenha o tempo de destino.  
  
> [!NOTE]  
>  As opções RESTORE_DATABASE e RESTORE_LOG point-in-time WITH são semelhantes, mas apenas RESTORE LOG é compatível com o argumento *mark_name*.  
  
 {STOPAT | STOPATMARK | STOPBEFOREMARK}   
 
 STOPAT **=** { **'**_datetime_**'** | **@**_datetime\_var* }  
 Especifica que o banco de dados seja restaurado para o estado em que estava na data e hora especificadas pelo parâmetro *datetime* ou **@**_datetime\_var_. Para obter informações sobre como especificar uma data e hora, consulte [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 Se uma variável for usada para STOPAT, a variável deverá ser um tipo de dados **varchar**, **char**, **smalldatetime** ou **datetime**. Apenas registros do log de transações gravados antes da data e hora especificadas são aplicados ao banco de dados.  
  
> [!NOTE]  
>  Se a hora STOPAT for após o último backup do LOG, o banco de dados será deixado no estado sem-recuperação, exatamente como se RESTORE LOG fosse executado com NORECOVERY.  
  
 Para obter mais informações, veja [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 STOPATMARK **=** { **'**_mark\_name_**'** | **'** lsn:_lsn\_number_**'** } [ AFTER **'**_datetime_**'** ]  
 Especifica recuperação para um ponto de recuperação especificado. A transação especificada é incluída na recuperação, mas ela será confirmada apenas se tiver sido confirmada originalmente quando foi realmente gerada.  
  
 RESTORE DATABASE e RESTORE LOG dão suporte ao parâmetro *lsn_number*. Esse parâmetro especifica um número de sequência de log.  
  
 Há compatibilidade com o parâmetro *mark_name* apenas na instrução RESTORE LOG. Esse parâmetro identifica uma marca de transação no backup de log.  
  
 Em uma instrução RESTORE LOG, se AFTER *datetime* for omitido, a recuperação será interrompida na primeira marca com o nome especificado. Se AFTER *datetime* for especificado, a recuperação será interrompida na primeira marca que tem o nome especificado exatamente ou após *datetime*.  
  
> [!NOTE]  
>  Se a marca especificada, LSN ou hora for após o último backup do LOG, o banco de dados será deixado no estado não recuperado, exatamente como se RESTORE LOG fosse executado com NORECOVERY.  
  
 Para obter mais informações, consulte [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) e [Recuperar para um número de sequência de log &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md).  
  
 STOPBEFOREMARK **=** { **'**_mark\_name_**'** | **'** lsn:_lsn\_number_**'** } [ AFTER **'**_datetime_**'** ]  
 Especifica recuperação até o ponto de recuperação especificado. A transação especificada não é incluída na recuperação e é revertida quando WITH RECOVERY for usado.  
  
 RESTORE DATABASE e RESTORE LOG dão suporte ao parâmetro *lsn_number*. Esse parâmetro especifica um número de sequência de log.  
  
 Há compatibilidade com o parâmetro *mark_name* apenas na instrução RESTORE LOG. Esse parâmetro identifica uma marca de transação no backup de log.  
  
 Em uma instrução RESTORE LOG, se AFTER *datetime* for omitido, a recuperação será interrompida exatamente antes da primeira marca com o nome especificado. Se AFTER *datetime* for especificado, a recuperação será interrompida logo antes da primeira marca que tem o nome especificado exatamente ou após *datetime*.  
  
> [!IMPORTANT]  
>  Se uma sequência de restauração parcial excluir qualquer grupo de arquivos FILESTREAM, não haverá suporte para a restauração point-in-time. Você pode forçar a sequência de restauração a continuar. Contudo, os grupos de arquivos FILESTREAM omitidos da instrução RESTORE nunca poderão ser restaurados. Para forçar uma restauração point-in-time, especifique a opção CONTINUE_AFTER_ERROR junto com a opção STOPAT, STOPATMARK ou STOPBEFOREMARK. Se você especificar CONTINUE_AFTER_ERROR, a sequência de restauração parcial terá êxito e o grupo de arquivos FILESTREAM se tornará irrecuperável.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Para obter conjuntos de resultados, consulte os tópicos a seguir:  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
## <a name="remarks"></a>Remarks  
 Para obter comentários adicionais, consulte os tópicos a seguir:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="specifying-a-backup-set"></a>Especificando um conjunto de backup  
 Um *conjunto de backup* contém o backup de uma única operação de backup bem-sucedida. As instruções RESTORE, RESTORE FILELISTONLY, RESTORE HEADERONLY e RESTORE VERIFYONLY funcionam em um único conjunto de backups dentro do conjunto de mídias no dispositivo de backup ou dispositivos especificados. Você deve especificar o backup necessário de dentro do conjunto de mídias. Você pode obter o *backup_set_file_number* de um backup definido usando a instrução [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md) .  
  
 A opção para especificar o conjunto de backup para restauração é:  
  
 FILE **=**{ *backup_set_file_number* | **@**_backup\_set\_file\_number_ }  
  
 Em que *backup_set_file_number* indica a posição do backup no conjunto de mídias. Um *backup_set_file_number* igual a 1 (FILE = 1) indica o primeiro conjunto de backup na mídia de backup e um *backup_set_file_number* igual a 2 (FILE = 2) indica o segundo conjunto de backup, e assim por diante.  
  
 O comportamento dessa opção varia conforme a instrução, como descrito na seguinte tabela:  
  
|de|Comportamento da opção FILE do conjunto de backup|  
|---------------|-----------------------------------------|  
|RESTORE|O número do arquivo do conjunto de backup padrão é 1. Apenas uma opção FILE de conjunto de backup é permitida em uma instrução RESTORE. É importante especificar conjuntos de backup na ordem.|  
|RESTORE FILELISTONLY|O número do arquivo do conjunto de backup padrão é 1.|  
|RESTORE HEADERONLY|Por padrão, todos os conjuntos de backup no conjunto de mídias são processados. O conjunto de resultados de RESTORE HEADERONLY retorna informações sobre cada conjunto de backup, incluindo sua **Posição** no conjunto de mídias. Para retornar informações sobre um conjunto de backup especificado, use o número de sua posição como o valor de *backup_set_file_number* na opção FILE.<br /><br /> Observação: Para mídia de fita, RESTORE HEADER processa conjuntos de backup na fita carregada.|  
|RESTORE VERIFYONLY|O *backup_set_file_number* padrão é 1.|  
  
> [!NOTE]  
>  A opção FILE para especificar um conjunto de backup não está relacionada à opção FILE para especificar um arquivo de banco de dados, FILE **=** { *logical_file_name_in_backup* | **@**_logical\_file\_name\_in\_backup\_var_ }.  
  
## <a name="summary-of-support-for-with-options"></a>Resumo de suporte para opções WITH  
 As seguintes opções WITH são compatíveis apenas com a instrução RESTORE: BLOCKSIZE, BUFFERCOUNT, MAXTRANSFERSIZE, PARTIAL, KEEP_REPLICATION, { RECOVERY | NORECOVERY | STANDBY }, REPLACE, RESTART, RESTRICTED_USER e { STOPAT | STOPATMARK | STOPBEFOREMARK }  
  
> [!NOTE]  
>  A opção PARTIAL tem suporte apenas de RESTORE DATABASE.  
  
 A tabela a seguir lista as opções de WITH usadas por uma ou mais instruções e indica quais instruções oferecem suporte a cada opção. Uma marca de verificação (√) indica que uma opção tem suporte. Um traço (–) indica que a opção não tem suporte.  
  
|Opção WITH|RESTORE|RESTORE FILELISTONLY|RESTORE HEADERONLY|RESTORE LABELONLY|RESTORE REWINDONLY|RESTORE VERIFYONLY|  
|-----------------|-------------|--------------------------|------------------------|-----------------------|------------------------|------------------------|  
|{ CHECKSUM<br /><br /> &#124; NO_CHECKSUM }|√|√|√|√|-|√|  
|{ CONTINUE_AFTER_ERROR<br /><br /> &#124; STOP_ON_ERROR }|√|√|√|√|-|√|  
|FILE<sup>1</sup>|√|√|√|-|-|√|  
|LOADHISTORY|-|-|-|-|-|√|  
|MEDIANAME|√|√|√|√|-|√|  
|MEDIAPASSWORD|√|√|√|√|-|√|  
|MOVE|√|-|-|-|-|√|  
|PASSWORD|√|√|√|-|-|√|  
|{ REWIND &#124; NOREWIND }|√|Apenas REWIND|Apenas REWIND|Apenas REWIND|-|√|  
|STATS|√|-|-|-|-|√|  
|{ UNLOAD &#124; NOUNLOAD }|√|√|√|√|√|√|  
  
 <sup>1</sup> FILE **=**_backup\_set\_file\_number_, which is distinct from {FILE | FILEGROUP}.  
  
## <a name="permissions"></a>Permissões  
 Para permissões, consulte os tópicos a seguir:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)  
  
-   [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)  
  
-   [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte os tópicos a seguir:  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
-   [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  

