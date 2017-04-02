---
title: "Tarefa de Backup de Banco de Dados (Plano de Manuten&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.maint.maintplanproperties.logbackup.f1"
  - "sql13.swb.maint.backup.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Tarefa de Backup de Banco de Dados"
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
caps.latest.revision: 52
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Tarefa de Backup de Banco de Dados (Plano de Manuten&#231;&#227;o)
  Use a caixa de diálogo **Tarefa Fazer Backup de Banco de Dados** para adicionar uma tarefa de backup ao plano de manutenção. O backup do banco de dados é importante no caso de falha do sistema ou hardware (ou erros do usuário) que levem o banco de dados a ser danificado de alguma forma, exigindo assim que uma cópia de backup seja restaurada. Essa tarefa lhe permite executar arquivos completos, diferenciais, e grupos de arquivos e backups de log de transações.  
  
 **Para criar uma tarefa de banco de dados de backup**  
  
-   [Criar um plano de manutenção](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
## Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Nova**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Bancos de dados**  
 Especifique os bancos de dados afetados por essa tarefa. Quando selecionada, a lista suspensa fornece as seguintes opções: **Todos os bancos de dados**, **Todos os bancos de dados do sistema**, **Todos os bancos de dados de usuário**, **Esses bancos de dados específicos**.  
  
 **Todos os bancos de dados**  
 Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Todos os bancos de dados do sistema (mestre, msdb, modelo)**  
 Gere um plano de manutenção que execute tarefas de manutenção em relação a cada um dos bancos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhuma tarefa de manutenção é executada nos bancos de dados criados pelo usuário.  
  
 **Todos os bancos de dados de usuários (exceto mestre, modelo, msdb, tempdb)**  
 Gere um plano de manutenção que execute tarefas de manutenção em todos os bancos de dados criados por usuários. Nenhuma tarefa de manutenção é executada com os bancos de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Estes bancos de dados**  
 Gere um plano de manutenção que execute tarefas de manutenção somente nos bancos de dados selecionados. Pelo menos um banco de dados da lista deverá ser selecionado se esta opção for escolhida.  
  
 **Tipo de backup**  
 Exibe o tipo de backup a ser executado.  
  
 **Componente de backup**  
 Selecione **Banco de dados** para fazer o backup de todo o banco de dados. Selecione **Arquivo e grupos de arquivos** para fazer o backup de apenas uma parte do banco de dados. Se selecionado, forneça o nome do arquivo ou do grupo de arquivos. Quando vários bancos de dados são selecionados na caixa **Bancos de dados** , especifique apenas **Bancos de dados** para **Componentes de backup**. Para executar backups de arquivo ou grupo de arquivos, crie uma tarefa para cada banco de dados.  
  
 **O conjunto de backup vai expirar**  
 Especifica quando o conjunto de backup pode ser substituído por outro conjunto de backup.  
  
 **Fazer backup em**  
 Execute o backup do banco de dados para um arquivo ou fita. Somente dispositivos de fita anexados ao computador que contém o banco de dados estão disponíveis.  
  
 **Execute o banco de dados por um ou mais arquivos**  
 Clique em **Adicionar** para abrir a caixa de diálogo **Selecionar Destino do Backup** e fornecer um ou mais locais de disco ou dispositivo de fita.  
  
 **Se existirem arquivos de backup**  
 Selecione **Anexar** para adicionar esse backup ao final do arquivo. Selecione **Substituir**, para remover qualquer backup antigo do arquivo e substituí-lo por pelo backup novo.  
  
 **Crie um arquivo de backup para cada banco de dados**  
 Crie um arquivo de backup no local especificado na caixa de pasta. Um arquivo será criado para cada banco de dados selecionado.  
  
 **Crie um subdiretório para cada banco de dados**  
 Selecione para colocar cada banco de dados em uma subpasta.  
  
> [!IMPORTANT]  
>  Embora planos de manutenção possam criar subdiretórios, tarefas de manutenção não podem excluir subdiretórios. Esse recurso reduz a possibilidade de um ataque mal-intencionado que use a tarefa de Limpeza de Manutenção para excluir arquivos.  
  
> [!IMPORTANT]  
>  O subdiretório herda permissões do diretório pai. Restrinja permissões para evitar acesso não autorizado.  
  
 **Pasta**  
 Especifique a pasta para os arquivos de banco de dados automaticamente criados.  
  
 **Extensão de arquivo de backup**  
 Especifique a extensão a ser usada para os arquivos de backup. O valor padrão é **.bak**.  
  
 **Verificar integridade do backup**  
 Verifique se o conjunto de backup está completo e se todos os volumes estão legíveis.  
  
 **Fazer backup da parte final do log e deixar o banco de dados no estado de restauração**  
 Execute um backup de log como a última etapa antes de restaurar um banco de dados. Para obter mais informações, veja [Backups da parte final do log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 **Defina compactação de backup**  
 Em [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (ou em uma versão posterior), selecione um dos seguintes valores de [compactação de backup](../../relational-databases/backup-restore/backup-compression-sql-server.md):  
  
|||  
|-|-|  
|**Usar a configuração padrão do servidor**|Clique para usar o padrão do nível de servidor.<br /><br /> Esse padrão é definido pela opção de configuração do servidor **padrão de compactação de backup**. Para obter informações sobre como exibir a configuração atual dessa opção, veja [Exibir ou configurar a opção backup compression default de configuração de servidor](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Compactar backup**|Clique em compactar backup, independentemente do padrão do nível do servidor.<br /><br /> **\*\* Importante \*\*** Por padrão, a compactação aumenta consideravelmente o uso da CPU, e o consumo adicional da CPU por parte do processo de compactação pode afetar negativamente as operações simultâneas. Portanto, é recomendável criar backups compactados de baixa prioridade em uma sessão cujo uso da CPU é limitado pelo [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md). Para obter mais informações, consulte [Usar o Administrador de Recursos para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).|  
|**Não compactar o backup**|Clique em criar um backup não compactado, independentemente do padrão do nível do servidor.|  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] com a Autenticação do Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## Consulte também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  