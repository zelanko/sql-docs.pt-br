---
title: Tarefa Transferir Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b7e72842412f829a51a0c7befdea30818d903ac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512073"
---
# <a name="transfer-database-task"></a>Tarefa Transferir Banco de Dados
  A tarefa Transferir Banco de Dados transfere um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao contrário das outras tarefas que transferem apenas objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de cópia, a tarefa Transferir Banco de Dados pode copiar ou mover um banco de dados. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor.  
  
## <a name="offline-and-online-modes"></a>Modos offline e online  
 O banco de dados pode ser transferido usando o modo online ou offline. Quando você usa o modo online, o banco de dados permanece anexado e é transferido por meio do SQL Management Object (SMO) para copiar os objetos do banco de dados. Quando você usa o modo offline, o banco de dados é desanexado, os arquivos do banco de dados são copiados ou movidos e o banco de dados é anexado ao destino após a conclusão bem-sucedida da transferência. Se o banco de dados for copiado, ele será novamente anexado de forma automática à fonte, se a cópia for bem-sucedida. No modo offline, o banco de dados é copiado mais rapidamente, mas o banco de dados fica indisponível aos usuários durante a transferência.  
  
 O modo offline requer que você especifique os compartilhamentos de arquivos de rede nos servidores de origem e de destino que contêm os arquivos de banco de dados. Se a pasta for compartilhada e acessada pelo usuário, você poderá fazer referência ao compartilhamento de rede usando a sintaxe \\\nome_do_computador\Arquivos de Programas\minha_pasta\\. Caso contrário, você deverá usar a sintaxe \\\nome_do_computador\c$\Arquivos de Programas\minha_pasta\\. Para usar a última sintaxe, o usuário deve ter acesso à gravação para os compartilhamentos de rede de origem e destino.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>Transferência de banco de dados entre versões do SQL Server  
 A tarefa Transferir Banco de Dados pode transferir um banco de dados entre instâncias de versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventos  
 A tarefa Transferir Banco de Dados não informa o progresso incremental da transferência de mensagem de erro; informa somente conclusão 0% e 100 %.  
  
## <a name="execution-value"></a>Valor de execução  
 O valor da execução, definido na propriedade **ExecutionValue** da tarefa, retorna o valor 1, porque em contraste com outras tarefas de transferência, a tarefa Transferir Banco de Dados pode transferir somente um banco de dados.  
  
 Ao atribuir uma variável definida pelo usuário à propriedade **ExecValueVariable** da tarefa Transferir Banco de Dados, as informações sobre a transferência de mensagem de erro podem se tornar disponíveis a outros objetos no pacote. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Entradas de log  
 A tarefa Transferir Banco de Dados inclui as seguintes entradas de log personalizadas:  
  
-   SourceSQLServer    Esta entrada de log lista o nome do servidor de origem.  
  
-   DestSQLServer    Esta entrada de log lista o nome do servidor de destino.  
  
-   SourceDB    Esta entrada de log lista o nome do banco de dados que é transferido.  
  
 Além disso, uma entrada de log para o evento **OnInformation** é gravada quando o banco de dados de destino é substituído.  
  
## <a name="security-and-permissions"></a>Segurança e permissões  
 Para transferir um banco de dados usando o  modo offline, o usuário que executa o pacote deve ser um membro da função servidor sysadmin.  
  
 Para transferir um banco de dados usando o modo online, o usuário que executa o pacote deve ser um membro da função servidor sysadmin ou proprietário do banco de dados (dbo) do banco de dados selecionado.  
  
## <a name="configuration-of-the-transfer-database-task"></a>Configuração da tarefa Transferir Banco de Dados  
 Você pode especificar se a tarefa tentará se anexar novamente ao banco de dados de origem, se a transferência do banco de dados falhar.  
  
 A tarefa Transferir Banco de Dados também pode ser configurada para permitir a sobregravação de um banco de dados de destino que tenha o mesmo nome, substituindo o banco de dados de destino.  
  
 O banco de dados de origem também pode ser renomeado como parte do processo de transferência. Se desejar transferir um banco de dados para uma instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que já contenha um banco de dados com o mesmo nome, a renomeação do banco de dados de origem permitirá a transferência do banco de dados. Entretanto, os nomes dos arquivos do banco de dados também devem ser diferentes; se já existirem arquivos com os mesmos nomes no destino, a tarefa falhará.  
  
 Quando copiar um banco de dados, ele não poderá ser menor que o banco de dados **modelo** do servidor de destino. Você pode aumentar o tamanho do banco de dados para fazer a cópia ou reduzir o tamanho do **modelo**.  
  
 No tempo de execução, a tarefa Transferir Banco de Dados conecta-se aos servidores de origem e de destino usando um ou dois gerenciadores de conexões SMO. Quando você cria uma cópia de um banco de dados no mesmo servidor, somente um gerenciador de conexões SMO é exigido. Os gerenciadores de conexões SMO são configurados separadamente da tarefa Transferir Banco de Dados e, em seguida,  referenciadas na tarefa Transferir Banco de Dados. Os gerenciadores de conexões SMO especificam o servidor e o modo de autenticação a serem usados quando a tarefa acessar o servidor. Para obter mais informações, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>Configuração programática da tarefa Transferir Banco de Dados  
 Para obter mais informações sobre como definir essas propriedades programaticamente, clique no tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>Editor da Tarefa Transferir Banco de Dados (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** para nomear e descrever a tarefa Transferir Banco de Dados. A tarefa Transferir Banco de Dados copia ou move um bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor.   
  
### <a name="options"></a>Opções  
 **Nome**  
 Digite um nome exclusivo para a tarefa Transferir Banco de Dados. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Transferir Banco de Dados.  
  
## <a name="transfer-database-task-editor-databases-page"></a>Editor da Tarefa Transferir Banco de Dados (página Bancos de Dados)
  Use a página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** para especificar as propriedades para os bancos de dado de origem e de destino envolvidos na tarefa Transferir Banco de Dados. A tarefa Transferir Banco de Dados copia ou move um bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa tarefa também pode ser usada para copiar um banco de dados dentro do mesmo servidor.  
  
### <a name="options"></a>Opções  
 **SourceConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de origem.  
  
 **DestinationConnection**  
 Selecione um gerenciador de conexões SMO na lista ou clique em **\<Nova conexão...>** para criar uma nova conexão com o servidor de destino.  
  
 **DestinationDatabaseName**  
 Especifique o nome do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor de destino.  
  
 Para popular este campo automaticamente com o nome do banco de dados de origem, especifique o **SourceConnection** e **SourceDatabaseName** primeiro.  
  
 Para renomear o banco de dados no servidor de destino, digite o novo nome neste campo.  
  
 **DestinationDatabaseFiles**  
 Especifica os nomes e locais dos arquivos de banco de dados no servidor de destino.  
  
 Para popular este campo automaticamente com os nomes e locais de arquivo de banco de dados, especifique o **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** primeiro.  
  
 Para renomear os arquivos de banco de dados ou especificar os novos locais no servidor de destino, popule esse campo com as informações de banco de dados de origem e clique no botão Procurar. Na caixa de diálogo **Arquivos de banco de dados de destino** , edite o **Arquivo de Destino**, a **Pasta de Destino**ou o **Compartilhamento de Arquivos na Rede**.  
  
> [!NOTE]  
>  Se você localizar os arquivos de banco de dados usando o botão Procurar, o local de arquivo será inserido usando a notação da unidade local: por exemplo, c:\\. É possível substituir isso pela a notação de compartilhamento na rede, inclusive o nome do computador e o nome de compartilhamento. Se o compartilhamento administrativo padrão for usado, será necessário usar a notação de $ e ter acesso administrativo ao compartilhamento.  
  
 **DestinationOverwrite**  
 Especifique se o é possível substituir o banco de dados no servidor de destino.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|Substitui o banco de dados no servidor de destino.|  
|**Falso**|Não substitui o banco de dados no servidor de destino.|  
  
> [!CAUTION]  
>  Os dados no banco de dados do servidor de destino serão substituídos se você especificar **True** para **DestinationOverwrite**, o que pode resultar na perda de dados. Para evitar isso, faça backup do banco de dados do servidor de destino em outro local antes de executar a tarefa Transferir Banco de Dados.  
  
 **Ação**  
 Especifique se a tarefa vai **Copiar** ou **Mover** o banco de dados para o servidor de destino.  
  
 **Método**  
 Especifique se a tarefa será executada enquanto o banco de dados no servidor de origem estiver no modo online ou offline.  
  
 Para transferir um banco de dados usando o modo offline, é necessário que o usuário que executa o pacote seja um membro da função de servidor fixa **sysadmin** .  
  
 Para transferir um banco de dados usando o modo online, é necessário que o usuário que executa o pacote seja um membro da função de servidor fixa **sysadmin** ou o proprietário do banco de dados (**dbo**) do banco de dados selecionado.  
  
 **SourceDatabaseName**  
 Selecione o nome do banco de dados a ser copiado ou movido.  
  
 **SourceDatabaseFiles**  
 Clique no botão Procurar para selecionar os arquivos de banco de dados.  
  
 **ReattachSourceDatabase**  
 Especifique se a tarefa tentará anexar novamente o banco de dados de origem se ocorrer uma falha.  
  
 As opções desta propriedade estão listadas na seguinte tabela:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|Anexa novamente o banco de dados de origem.|  
|**Falso**|Não anexa novamente o banco de dados de origem.|  

## <a name="source-database-files"></a>Arquivos de banco de dados de origem
  Use a caixa de diálogo **Arquivos de Banco de Dados de Origem** para visualizar os nomes e locais do arquivo do banco de dados no servidor de origem ou especificar um local de compartilhamento de arquivos na rede para a tarefa Transferir Banco de Dados.   
  
 Para popular esta caixa de diálogo com os nomes e locais dos arquivos do banco de dados no servidor de origem, especifique primeiro **SourceConnection** e **SourceDatabaseName** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
### <a name="options"></a>Opções  
 **Arquivo de Origem**  
 Nomes do arquivo de banco de dados no servidor de origem que serão transferidos. O**Arquivo de Origem** é somente leitura.  
  
 **Pasta de Origem**  
 Pasta no servidor de origem em que residem os arquivos de banco de dados a serem transferidos. A**Pasta de Origem** é somente leitura.  
  
 **Compartilhamento de Arquivos na Rede**  
 Pasta de compartilhamento de rede no servidor de origem da qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de Arquivo na Rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira a localização de compartilhamento de arquivos na rede ou clique no botão Procurar **(...)** para localizá-la.  
  
 Na transferência de um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** no servidor de origem, antes de serem transferidos ao servidor de destino.  

## <a name="destination-database-files"></a>Arquivos de banco de dados de destino
  Use a caixa de diálogo **Arquivos do Banco de Dados de Destino** para exibir ou alterar os nomes e locais dos arquivos de banco de dados no servidor de destino ou especificar um local de arquivos na rede para a tarefa Transferir Banco de Dados.  
  
 Para popular automaticamente essa caixa de diálogo com os locais e nomes de arquivos no servidor de origem, especifique o **SourceConnection**, **SourceDatabaseName**, e **SourceDatabaseFiles** primeiro na página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
### <a name="options"></a>Opções  
 **Arquivo de Destino**  
 Nomes dos arquivos de banco de dados transferidos no servidor de destino.  
  
 Digite o nome do arquivo ou clique no nome do arquivo para editá-lo.  
  
 **Pasta de Destino**  
 Pasta no servidor de destino para onde os arquivos de banco de dados serão transferidos.  
  
 Digite o caminho da pasta, clique no caminho da pasta para editá-lo ou clique em procurar para localizar a pasta onde você quer transferir os arquivos de banco de dados no servidor de destino.  
  
 **Compartilhamento de Arquivos na Rede**  
 Pasta compartilhada de rede no servidor de destino para o qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de arquivo na rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira o local de compartilhamento de arquivos na rede ou clique em Procurar para localizá-lo.  
  
 Ao transferir um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** antes de serem transferidos para o local **Pasta de destino** .  
