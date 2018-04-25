---
title: Utilitário Sqlmaint | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sqlmaint
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database maintenance plans [SQL Server]
- sqlmaint utility
- maintaining databases [SQL Server]
- backups [SQL Server], sqlmaint utility
- command prompt utilities [SQL Server], sqlmaint
- maintenance plans [SQL Server], command prompt
- backing up [SQL Server], sqlmaint utility
ms.assetid: 937a9932-4aed-464b-b97a-a5acfe6a50de
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5384932d020b62b3e88d28cc37e3155a4a72f6ee
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="sqlmaint-utility"></a>utilitário sqlmaint
O utilitário[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]sqlmaint** executa um conjunto especificado de operações de manutenção em um ou mais bancos de dados. Use o **sqlmaint** para executar verificações DBCC, fazer backup de um banco de dados e do respectivo log de transações, atualizar estatísticas e recompilar índices. Todas as atividades de manutenção de banco de dados geram um relatório que pode ser enviado a um arquivo de texto designado, arquivo HTML ou conta de email. O**sqlmaint** executa planos de manutenção de bancos de dados criados com versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para executar planos de manutenção do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no prompt de comando, use o [Utilitário dtexec](../integration-services/packages/dtexec-utility.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../includes/ssnotedepnextavoid-md.md)] Em vez disso, use o recurso de plano de manutenção do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações sobre planos de manutenção, veja [Planos de manutenção](../relational-databases/maintenance-plans/maintenance-plans.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlmaint   
[-?] |  
[  
     [-S server_name[\instance_name]]  
     [-U login_ID [-P password]]  
     {  
          [-D database_name | -PlanName name | -PlanID guid ]  
          [-Rpt text_file]  
          [-To operator_name]  
          [-HtmlRpt html_file [-DelHtmlRpt <time_period>] ]  
          [-RmUnusedSpace threshold_percentfree_percent]  
          [-CkDB | -CkDBNoIdx]  
          [-CkAl | -CkAlNoIdx]  
          [-CkCat]  
          [-UpdOptiStats sample_percent]  
          [-RebldIdx free_space]  
          [-SupportComputedColumn]  
          [-WriteHistory]  
          [  
               {-BkUpDB [backup_path] | -BkUpLog [backup_path] }  
               {-BkUpMedia  
                    {DISK [  
                           [-DelBkUps <time_period>]   
                           [-CrBkSubDir ]   
                           [-UseDefDir ]   
                          ]  
                     | TAPE   
                    }  
               }  
               [-BkUpOnlyIfClean]  
               [-VrfyBackup]  
          ]  
     }  
]  
<time_period> ::=  
number[minutes | hours | days | weeks | months]  
```  
  
## <a name="arguments"></a>Argumentos  
 Os parâmetros e seus valores devem ser separados por um espaço. Por exemplo, deve haver um espaço entre **-S** e *server_name*.  
  
 **-?**  
 Especifica que o diagrama de sintaxe para o **sqlmaint** seja retornado. Este parâmetro deve ser usado sozinho.  
  
 **-S** *server_name*[ *\\* instance_name]  
 Especifica a instância de destino do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especifica *server_name* para a conexão com a instância padrão do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] nesse servidor. Especifique *server_name***\\****[!INCLUDE[ssDE](../includes/ssde-md.md)]instance_name para se conectar a uma instância nomeada do  nesse servidor. Se nenhum servidor for especificado, o **sqlmaint** se conecta à instância padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)] no computador local.  
  
 **-U** *login_ID*  
 Especifica a ID de logon a ser usada para se conectar ao servidor. Se não for fornecida, o **sqlmaint** tenta usar a [!INCLUDE[msCoName](../includes/msconame-md.md)] -Windows-Authentication. Se *login_ID* contiver caracteres especiais, ele deverá estar entre aspas duplas ("); caso contrário, as aspas duplas serão opcionais.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows.  
  
 **-P** *password*  
 Especifica a senha para a ID de logon. Válido somente se o parâmetro **-U** também for fornecido. Se o *password* contiver caracteres especiais, ele deve estar entre aspas duplas; caso contrário, as aspas duplas são opcionais.  
  
> [!IMPORTANT]  
>  A senha não é mascarada. Quando possível, use a Autenticação do Windows.  
  
 **-D** *database_name*  
 Especifica o nome do banco de dados no qual a operação de manutenção deve ser executada. Se o *database_name* contiver caracteres especiais, ele deverá estar entre aspas duplas; caso contrário, as aspas duplas são opcionais.  
  
 **-PlanName** *name*  
 Especifica o nome de um plano de manutenção de banco de dados definido com o uso do Assistente para Planos de Manutenção de Banco de Dados. A única informação que **sqlmaint** usa do plano é a lista de bancos de dados. Todas as atividades de manutenção especificadas nos outros parâmetros do **sqlmaint** se aplicam a esta lista de bancos de dados.  
  
 **-PlanID** *guid*  
 Especifica o identificador global exclusivo (GUID) de um plano de manutenção de banco de dados definido com o uso do Assistente para Planos de Manutenção de Banco de Dados. A única informação que **sqlmaint** usa do plano é a lista de bancos de dados. Todas as atividades de manutenção especificadas nos outros parâmetros do **sqlmaint** se aplicam a esta lista de bancos de dados. Isso deve corresponder a um valor do plan_id em msdb.dbo.sysdbmaintplans.  
  
 **-Rpt** *text_file*  
 Especifica o caminho completo e o nome do arquivo no qual será gerado o relatório. O relatório também é gerado na tela. O relatório mantém informações de versão adicionando uma data ao nome do arquivo. A data é gerada da seguinte forma: ao final do nome do arquivo, mas antes do ponto final, no formato _*aaaaMMddhhmm*. *aaaa* = ano, *MM* = mês, *dd* = dia, *hh* = hora, *mm* = minuto.  
  
 Se você executar o utilitário às 10h23 em 1º de dezembro de 1996, e esse é o valor de *text_file* :  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.rpt  
```  
  
 O nome de arquivo gerado é:  
  
```  
c:\Program Files\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint_199612011023.rpt  
```  
  
 O nome do arquivo UNC completo é necessário para *text_file* , quando **sqlmaint** acessa um servidor remoto.  
  
 **-To**  *operator_name*  
 Especifica o operador para quem o relatório gerado será enviado por meio do SQL Mail.  
  
 **-HtmlRpt** *html_file*  
 Especifica o caminho completo e nome do arquivo no qual um relatório HTML será gerado. **sqlmaint** gera o nome de arquivo, acrescentando uma cadeia de caracteres no formato _*aaaaMMddhhmm* ao nome do arquivo, da mesma forma que faz para o parâmetro **-Rpt** .  
  
 O nome do arquivo UNC completo é necessário para *html_file* , quando **sqlmaint** acessa um servidor remoto.  
  
 **-DelHtmlRpt** \<*time_period*>  
 Especifica que qualquer relatório HTML no diretório de relatórios deverá ser excluído se o intervalo de tempo depois da criação do arquivo de relatório exceder <\<time_period *>. **-DelHtmlRpt** procura arquivos cujos nomes correspondem ao padrão gerado pelo parâmetro *html_file*. Se *html_file* for c:\Arquivos de Programas\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint.htm, **-DelHtmlRpt** fará com que **sqlmaint** exclua todos os arquivos cujos nomes correspondem ao padrão C:\Arquivos de Programas\Microsoft SQL Server\Mssql\Backup\AdventureWorks2012_maint\*.htm e que sejam anteriores ao <\<time_period *> especificado.  
  
 **-RmUnusedSpace** *threshold_percent free_percent*  
 Especifica que o espaço não usado seja removido do banco de dados especificado em **-D**. Essa opção só é útil para bancos de dados definidos para crescer automaticamente. *Threshold_percent* especifica o tamanho em megabytes que o banco de dados deve atingir, antes que **sqlmaint** tente remover o espaço de dados não utilizado. Se o banco de dados for menor que *threshold_percent*, nenhuma ação será tomada. *Free_percent* especifica quanto espaço não utilizado deve permanecer no banco de dados, especificado como um percentual do tamanho final do banco de dados. Por exemplo, se um banco de dados com 200 MB contiver 100 MB de dados, especificar 10 para *free_percent* resultará em um tamanho final de banco de dados de 110 MB. Observe que um banco de dados não será expandido se for menor do que *free_percent* somado à quantidade de dados no banco de dados. Por exemplo, se um banco de dados de 108 MB tiver 100 MB de dados, especificar 10 para *free_percent* não expandirá o banco de dados para 110 MB; ele permanecerá com 108 MB.  
  
 **-CkDB** | **-CkDBNoIdx**  
 Especifica que uma instrução DBCC CHECKDB ou DBCC CHECKDB com a opção de NOINDEX seja executada no banco de dados especificado em **-D**. Para obter mais informações, consulte DBCC CHECKDB.  
  
 Um aviso será gravado em *text_file* , se o banco de dados estiver em uso, quando **sqlmaint** for executado.  
  
 **-CkAl** | **-CkAlNoIdx**  
 Especifica que uma instrução DBCC CHECKALLOC com a opção de NOINDEX seja executada no banco de dados especificado em **-D**. Para obter mais informações, veja [DBCC CHECKALLOC &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md).  
  
 **-CkCat**  
 Especifica que uma instrução DBCC CHECKCATALOG (Transact-SQL) seja executada no banco de dados especificado em **-D**. Para obter mais informações, veja [DBCC CHECKCATALOG &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md).  
  
 **-UpdOptiStats** *sample_percent*  
 Especifica que a instrução seguinte seja executada em cada tabela no banco de dados:  
  
```  
UPDATE STATISTICS table WITH SAMPLE sample_percent PERCENT;  
```  
  
 Se as tabelas incluírem colunas computadas, também será necessário especificar o argumento **-SupportedComputedColumn** quando usar **-UpdOptiStats**.  
  
 Para obter mais informações, veja [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md).  
  
 **-RebldIdx** *free_space*  
 Especifica que os índices nas tabelas do banco de dados de destino devem ser reconstruídos usando o valor percentual de *free_space* como o inverso do fator de preenchimento. Por exemplo, se o percentual de *free_space* for 30, o fator de preenchimento usado será 70. Se for especificado um valor percentual de *free_space* de 100, os índices serão reconstruídos com o fator de preenchimento original.  
  
 Se os índices estiverem em colunas computadas, também será necessário especificar o argumento **-SupportComputedColumn** quando usar **-RebldIdx**.  
  
 **-SupportComputedColumn**  
 Deve ser especificado para executar comandos de manutenção DBCC com **sqlmaint** em colunas computadas.  
  
 **-WriteHistory**  
 Especifica que deve haver uma entrada em msdb.dbo.sysdbmaintplan_history para cada ação de manutenção executada por **sqlmaint**. Se **-PlanName** ou **-PlanID** for especificado, as entradas no sysdbmaintplan_history usarão a ID do plano especificado. Se **-D** for especificado, as entradas em sysdbmaintplan_history serão feitas com zeros para a ID do plano.  
  
 **-BkUpDB** [ *backup_path*] |  **-BkUpLog** [ *backup_path* ]  
 Especifica uma ação de backup. **-BkUpDb** faz o backup de todo o banco de dados. **-BkUpLog** faz backup apenas do log de transações.  
  
 *backup_path* especifica o diretório do backup. *backup_path* não será necessário se **-UseDefDir** também for especificado e será substituído por **-UseDefDir** se ambos estiverem especificados. O backup pode ser colocado em um diretório ou em um endereço de dispositivo de fita (por exemplo, \\\\.\TAPE0). O nome do arquivo para um backup de banco de dados é gerado automaticamente como segue:  
  
```  
dbname_db_yyyyMMddhhmm.BAK  
  
```  
  
 onde  
  
-   *dbname* é o nome do banco de dados do qual é feito o backup.  
  
-   *aaaaMMddhhmm* é o tempo da operação de backup com *aaaa* = ano, *MM* = mês *dd* = dia, *hh* = hora e *mm* = minuto.  
  
 O nome do arquivo para um backup de transações é gerado automaticamente com um formato semelhante:  
  
```  
dbname_log_yyyymmddhhmm.BAK  
  
```  
  
 Se usar o parâmetro **-BkUpDB** , também será necessário especificar a mídia usando o parâmetro **-BkUpMedia** .  
  
 **-BkUpMedia**  
 Especifica o tipo de mídia do backup: DISK ou TAPE.  
  
 **DISK**  
 Especifica que a mídia de backup é disco.  
  
 **-DelBkUps**< *time_period* >  
 Para backups em disco, especifica que qualquer arquivo de backup no diretório de backups deverá ser excluído se o intervalo de tempo depois da criação do backup exceder o <\<time_period *>.  
  
 **-CrBkSubDir**  
 Para backups em disco, especifica que um subdiretório deverá ser criado no diretório [*backup_path*] ou no diretório de backup padrão se o **-UseDefDir** também for especificado. O nome do subdiretório é gerado com base no nome do banco de dados especificado em **-D**. **-CrBkSubDir** oferece um modo fácil de colocar todos os backups de bancos de dados diferentes em subdiretórios separados, sem a necessidade de alterar o parâmetro *backup_path* .  
  
 **-UseDefDir**  
 Para backups de disco, especifica que o arquivo de backup seja criado no diretório padrão de backup. **UseDefDir** substituirá *backup_path* se ambos forem especificados. Com uma instalação padrão do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o diretório padrão de backup é C:\Arquivos de Programas\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Backup.  
  
 **TAPE**  
 Especifica que a mídia de backup é fita.  
  
 **-BkUpOnlyIfClean**  
 Especifica que o backup ocorrerá apenas se nenhuma verificação **-Ck** especificada encontrar problemas nos dados. As ações de manutenção são executadas na mesma sequência em que aparecem no prompt de comando. Especifique o parâmetro **-CkDB**, **-CkDBNoIdx**, **-CkAl**, **-CkAlNoIdx**, **-CkTxtAl**ou **-CkCat** antes de **-BkUpDB**/**-BkUpLog** caso também for especificar **-BkUpOnlyIfClean**, ou o backup ocorrerá independentemente de a verificação relatar problemas ou não.  
  
 **-VrfyBackup**  
 Especifica que o RESTORE VERIFYONLY será executado no backup quando este for concluído.  
  
 *number*[**minutes**| **hours**| **day**| **weeks**| **months**]  
 Especifica o intervalo de tempo usado para determinar se um relatório ou arquivo de backup é antigo o bastante para ser excluído. *number* é um inteiro seguido (sem espaço) por uma unidade de tempo. Exemplos válidos:  
  
-   **12semanas**  
  
-   **3meses**  
  
-   **15dias**  
  
 Se apenas o *number* for especificado, a parte de data padrão será **weeks**.  
  
## <a name="remarks"></a>Remarks  
 O utilitário **sqlmaint** executa operações de manutenção em um ou mais bancos de dados. Se **-D** for especificado, as operações especificadas nas demais opções serão executadas apenas no banco de dados especificado. Se **-PlanName** ou **-PlanID** forem especificados, a única informação que **sqlmaint** recuperará do plano de manutenção especificado será a lista de bancos de dados no plano. Todas as operações especificadas nos demais parâmetros do **sqlmaint** são aplicadas a cada banco de dados na lista obtida do plano. O utilitário **sqlmaint** não aplica atividades de manutenção definidas no próprio plano.  
  
 O utilitário **sqlmaint** retorna 0 se for executado com êxito ou 1 se apresentar falha. A falha é informada:  
  
-   Se alguma ação de manutenção apresentar falha.  
  
-   Se as verificações **-CkDB**, **-CkDBNoIdx**, **-CkAl**, **-CkAlNoIdx**, **-CkTxtAl**ou **-CkCat** encontrarem problemas nos dados.  
  
-   Se uma falha geral for encontrada.  
  
## <a name="permissions"></a>Permissões  
 O utilitário **sqlmaint** pode ser executado por qualquer usuário do Windows com a permissão **Ler e Executar** no `sqlmaint.exe`que, por padrão, é armazenado na pasta `x:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER1\MSSQL\Binn` . Adicionalmente, o logon [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificado com **-ID_logon** deve ter as permissões exigidas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para executar a ação especificada. Se a conexão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar a autenticação do Windows, o logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mapeado para autenticar o usuário do Windows deve ter as permissões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exigidas para realizar a ação especificada.  
  
 Por exemplo, o uso de **-BkUpDB** exige permissão para executar a instrução BACKUP. Além disso, o uso do argumento **-UpdOptiStats** exige permissão para executar a instrução UPDATE STATISTICS. Para obter mais informações, consulte as seções "Permissões" dos tópicos correspondentes nos Manuais Online.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-performing-dbcc-checks-on-a-database"></a>A. Realização de verificações DBCC em um banco de dados  
  
```  
sqlmaint -S MyServer -D AdventureWorks2012 -CkDB -CkAl -CkCat -Rpt C:\MyReports\AdvWks_chk.rpt  
```  
  
### <a name="b-updating-statistics-using-a-15-sample-in-all-databases-in-a-plan-also-shrink-any-of-the-database-that-have-reached-110-mb-to-having-only-10-free-space"></a>B. Atualização de estatísticas usando uma amostra de 15% em todos os bancos de dados em um plano. Também, reduz qualquer banco de dados que tenha alcançado 110 MB para ter só 10% de espaço livre.  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -UpdOptiStats 15 -RmUnusedSpace 110 10  
```  
  
### <a name="c-backing-up-all-the-databases-in-a-plan-to-their-individual-subdirectories-in-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory-also-delete-any-backups-older-than-2-weeks"></a>C. Realização de backup de todos os bancos de dados em um plano nos respectivos subdiretórios individuais no diretório padrão x:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Diretório de backup. Exclui também qualquer backup com mais de 2 semanas  
  
```  
sqlmaint -S MyServer -PlanName MyUserDBPlan -BkUpDB -BkUpMedia DISK -UseDefDir -CrBkSubDir -DelBkUps 2weeks  
```  
  
### <a name="d-backing-up-a-database-to-the-default-xprogram-filesmicrosoft-sql-servermssql13mssqlservermssqlbackup-directory"></a>D. Realização de backup de um banco de dados no diretório padrão x:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Diretório de backup.\  
  
```  
sqlmaint -S MyServer -BkUpDB -BkUpMedia DISK -UseDefDir  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../t-sql/statements/backup-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../t-sql/statements/update-statistics-transact-sql.md)  
  
  
