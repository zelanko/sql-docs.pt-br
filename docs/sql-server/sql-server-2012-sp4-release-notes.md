---
title: Notas de versão do SQL Server 2012 Service Pack | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-non-specified
ms.technology: supportability
ms.custom: ''
ms.date: 2/26/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
monikerRange: = sql-server-2014 || = sqlallproducts-allversions
ms.openlocfilehash: c89264e120ce67a814d102f0306f74e06c3d79f8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="sql-server-2012-service-pack-release-notes"></a>Notas de versão do SQL Server 2012 Service Pack
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Este tópico contém as notas de versão agregadas dos quatro service packs do SQL Server 2012. Cada service pack acumula os service packs anteriores.

Os services packs estão disponíveis somente online, não em uma mídia de instalação e podem ser baixados da seguinte maneira:
- [SQL Server 2012 SP4 ](https://go.microsoft.com/fwlink/?linkid=846937)
- [SQL Server 2012 SP3](http://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)
- [SQL Server 2012 SP2](http://support.microsoft.com/KB/2958429)
- [SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268158)

## <a name="service-pack-4-release-notes"></a>Notas de versão do Service Pack 4

### <a name="download-pages"></a>Páginas de download

- [Feature Pack do Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846907)
- [Instalação de Patch do SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)


### <a name="performance-and-scale-improvements"></a>Melhorias de desempenho e escalabilidade
- **Melhoria no procedimento de limpeza do agente de distribuição** – Um banco de dados de distribuição muito grande causou a situação de bloqueio e de deadlock. Um procedimento de limpeza aprimorado tem como objetivo eliminar alguns desses cenários de bloqueio ou de deadlock. 
- **Dimensionamento do Objeto de Memória Dinâmica** – Particione dinamicamente objetos de memória com base em inúmeros nós e núcleos a serem dimensionados no hardware moderno. A meta da promoção dinâmica é evitar possíveis gargalos e particionar automaticamente um objeto de memória thread-safe. Objetos de memória não particionados podem ser promovidos dinamicamente para serem particionados por nó. O número de partições é igual ao número de nós NUMA. Objetos de memória particionados por nó podem ser promovidos mais ainda para serem particionado por CPU, em que o número de partições é igual ao número de CPUs.
- **Habilitar > 8TB para o Pool de buffers** – Habilite um espaço de endereço virtual de 128 TB para uso do pool de buffers
- **Limpeza do controle de alterações** – Melhoria do desempenho e da eficiência da limpeza de controle de alterações para tabelas laterais do Controle de Alterações. 

### <a name="supportability-and-diagnostics-improvements"></a>Melhorias de diagnóstico e da capacidade de suporte
- **Suporte de despejos completos para Agentes de Replicação** – Atualmente, se os agentes de replicação encontram uma exceção sem tratamento, o comportamento padrão é criar um minidespejo dos sintomas da exceção. O comportamento padrão requer uma etapa de solução de problemas complexos para exceções sem tratamento. O SP4 introduz uma nova chave do Registro, que é compatível com a criação de um despejo completo para os Agentes de replicação.
- **Aprimoramento do diagnóstico no XML do plano de execução** – O XML do plano de execução foi aprimorado para expor informações sobre sinalizadores de rastreamento, frações de memória para junção de loop aninhada, tempo da CPU e tempo decorrido habilitados. 
- **Melhoria na correlação entre DMVs e XE de diagnóstico** – Os campos Query_hash e query_plan_hash são usados para identificar uma consulta com exclusividade. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL Server não tem “bigint sem sinal”, a conversão nem sempre funciona. Essa melhoria introduz novas colunas de filtro/ação XEvent equivalentes a query_hash e a query_plan_hash, exceto que elas estão definidas como INT64, o que podem ajudar a correlacionar consultas entre XE e DMVs. 
- **Melhor diagnóstico de uso/concessão de memória** – Novo XEvent query_memory_grant_usage (backport do Server 2016 SP1)
- **Adicionar o rastreamento de protocolo a etapas de negociação SSL** – Adicione informações de rastreamento de bit para negociação com êxito/falha, incluindo o protocolo etc. Pode ser útil ao solucionar problemas de cenários de conectividade ao mesmo tempo, por exemplo, que a implantação do TLS 1.2
- **Configuração do nível de compatibilidade correto para o banco de dados de distribuição** – Após a instalação do Service Pack, o nível de compatibilidade do banco de dados de distribuição é alterado para 90. A alteração do nível ocorreu devido a um problema no procedimento armazenado de sp_vupgrade_replication. Agora o SP foi alterado para definir o nível de compatibilidade correto para o banco de dados de distribuição. 
- **Novo comando DBCC para clonar um banco de dados** – O banco de dados clonado é um novo comando DBCC adicionado que permite que usuários avançados, como CSS, solucionem problemas em bancos de dados de produção existentes por meio da clonagem do esquema e dos metadados, sem os dados. A chamada é realizada com clonedatabase DBCC (‘source_database_name’, ‘clone_database_name’). Os bancos de dados clonados não devem ser usados em ambientes de produção. Para ver se um banco de dados foi gerado de uma chamada para o banco de dados clonado, é possível usar o seguinte comando, selecione DATABASEPROPERTYEX('clonedb', 'isClone'). O valor retornado de 1 é true e 0 é false. 
- **Arquivo TempDB e informações de tamanho do arquivo no Log de erros do SQL** – Se o tamanho e o crescimento automático forem diferentes para os arquivos de dados TempDB durante a inicialização, imprima o número de arquivos e dispare um aviso.
- **Mensagens de suporte da IFI no Log de erros do SQL Server** – No log de erros, indique que a Inicialização Instantânea de Arquivo está habilitada/desabilitada
- **Novo DMF para substituir o DBCC INPUTBUFFER** – Uma nova Função de gerenciamento dinâmico sys.dm_input_buffer que usa o session_id como parâmetro é introduzida para substituir DBCC INPUTBUFFER
- **Aprimoramento de XEvents para falha na leitura de roteamento para um Grupo de disponibilidade** – No momento, o XEvent read_only_rout_fail só será acionado se houver uma lista de roteamento presente, mas nenhum dos servidores na lista de roteamento estará disponível para conexões. Essa melhoria inclui informações adicionais para ajudar a solucionar problemas e também é expandida nos pontos de código em que o XEvent é acionado. 
- **Melhoria no tratamento do Service Broker com o failover do grupo de disponibilidade** – No momento, quando o Service Broker é habilitado em Banco de dados do gruo de disponibilidade, durante um failover do grupo de disponibilidade, todas as conexões do Service Broker originadas na Réplica Primária são deixadas abertas. A melhoria fecha todas essas conexões abertas durante um failover do grupo de disponibilidade.
- **Particionamento do soft-NUMA automático** – com o SQL 2014 SP2, o particionamento [Soft-NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) automático é introduzido quando o sinalizador de rastreamento 8079 é habilitado no nível do servidor. Quando o Sinalizador de rastreamento 8079 é habilitado durante a inicialização, o SQL Server 2014 SP2 interroga o layout de hardware e configura automaticamente o soft-NUMA em sistemas que reportam oito ou mais CPUs por nó NUMA. O comportamento do soft-NUMa automático tem reconhecimento de hyperthread (HT/processador lógico). O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável testar primeiro o desempenho da carga de trabalho com o soft-NUMA automático antes que ele seja ATIVADO na produção.

## <a name="service-pack-3-release-notes"></a>Notas de versão do Service Pack 3

### <a name="download-pages"></a>Páginas de download
- [Feature Pack do SQL Server 2012 SP3](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

Para obter mais informações detalhadas para identificar o local e o nome do arquivo a ser baixado com base na versão instalada no momento, consulte a seção “Selecionar o arquivo correto a ser baixado” em [Informações de versão do SQL Server 2012 Service Pack 3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information).

## <a name="service-pack-2-release-notes"></a>Notas de versão do Service Pack 2
  
### <a name="download-pages"></a>Páginas de download 
- [Feature Pack do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

Use a tabela abaixo para identificar o local e o nome do arquivo a ser baixado com base em sua versão atualmente instalada. As páginas de download têm requisitos de sistema e instruções básicas de instalação.  

|Se a versão instalada atual for...|E você quiser...|Baixar e instalar...|  
|---|---|---|   
|Instalações de 32 bits:|||  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 32 bits do SQL Server 2012 SP2|**SQLServer2012SP2-KB2958429-**<arch>**-**<lang id>**.exe** da [página de download do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Uma versão de 32 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 32 bits do SQL Server 2012 Express SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de somente ferramentas do cliente e de gerenciamento para SQL Server 2012 (incluindo SQL Server 2012 Management Studio)|Atualizar o cliente e as ferramentas de gerenciamento para a versão de 32 bits do SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits do SQL Server 2012 Management Studio Express|Atualizar para a versão de 32 bits do SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012 e uma versão de 32 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 32 bits do SQL Server 2012 SP2|**SQLEXPRADV_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express.](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) ou [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Atualizar as ferramentas para a versão de 32 bits do Microsoft SQL Server 2012 SP2 Feature Pack|Uma ou mais ferramentas na página de download do Microsoft [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|  
|Instalações de 64 bits:|||  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 64 bits do SQL Server 2012 SP2|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe da [página de download do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Uma versão de 64 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits com somente o cliente e as ferramentas de gerenciamento para SQL Server 2012 SQL (incluindo SQL Server 2012 Management Studio)|Atualizar as ferramentas de cliente e gerenciamento para a versão de 64 bits do SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits do SQL Server 2012 Management Studio Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) ou [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Atualizar as ferramentas para a versão de 64 bits do Microsoft SQL Server 2012 SP2 Feature Pack|Uma ou mais ferramentas na página de download do Microsoft [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|   


## <a name="service-pack-1-release-notes"></a>Notas de versão do Service Pack 1

### <a name="download-pages"></a>Páginas de download  
- [Feature Pack do SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268158)
- [SQL Server 2012 SP1 Express](http://go.microsoft.com/fwlink/p/?LinkID=26815)


Use a tabela a seguir para determinar qual arquivo baixar e instalar. Verifique se você tem os requisitos de sistema corretos antes de instalar o service pack. Os requisitos de sistemas são fornecidos nas páginas de download vinculadas na tabela.  

|Se a versão instalada atual for...|E você quiser...|Baixar e instalar...|  
|---|---|---|  
|**Instalações de&32; bits:**|||  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 32 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 32 bits do SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 bits de somente ferramentas do cliente e de gerenciamento para SQL Server 2012 (incluindo SQL Server 2012 Management Studio)|Atualizar as ferramentas do cliente e de gerenciamento para a versão de 32 bits do SQL Server 2012 SP1|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 32 bits do SQL Server 2012 Management Studio Express|Atualizar a versão de 32 bits do SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012 **e** uma versão de 32 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 32 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 32 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=16978)|Atualizar as ferramentas para a versão de 32 bits do Microsoft SQL Server 2012 SP1 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Nenhuma instalação de 32 bits do SQL Server 2012|Instalar a versão de 32 bits do SQL Server 2012 incluindo o SP1 (nova instância com SP1 pré-instalado)|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x86-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Nenhuma instalação de 32 bits do SQL Server 2012 Management Studio|Instalar a versão de 32 bits do SQL Server 2012 Management Studio incluindo SP1|SQLManagementStudio_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Nenhuma versão de 32 Bits do SQL Server 2012 RTM Express|Instalar a versão de 32 bits do SQL Server 2012 Express incluindo SP1|SQLEXPR32_x86_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Uma instalação de 32 bits do **SQL Server 2008** ou do **SQL Server 2008 R2**|**Atualização in-loco** para a versão de 32 bits do SQL Server 2012 com SP1|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x86-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**Instalações de&64; bits:**|||  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 bits com somente o cliente e as ferramentas de gerenciamento para SQL Server 2012 SQL (incluindo SQL Server 2012 Management Studio)|Atualizar o cliente e as ferramentas de gerenciamento para a versão de 64 bits do SQL Server 2012 SP1|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 64 bits do SQL Server 2012 Management Studio Express|Atualizar a versão de 64 bits do SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012 **e** uma versão de 64 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 64 bits do SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Uma versão de 64 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/en/details.aspx?id=16978)|Atualizar as ferramentas para a versão de 64 bits do Microsoft SQL Server 2012 SP1 Feature Pack|Um ou mais arquivos do [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Nenhuma instalação de 64 bits do SQL Server 2012|Instalar a versão de 64 bits do SQL Server 2012 incluindo o SP1 (nova instância com SP1 pré-instalado)|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x64-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Nenhuma instalação de 64 bits do SQL Server 2012 Management Studio|Instalar a versão de 64 bits do SQL Server 2012 Management Studio incluindo SP1|SQLManagementStudio_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Nenhuma versão de 64 Bits do SQL Server 2012 RTM Express|Instalar a versão de 64 bits do SQL Server 2012 Express incluindo SP1|SQLEXPR_x64_ENU.exe [aqui](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Uma instalação de 64 bits do **SQL Server 2008** ou do **SQL Server 2008 R2**|**Atualização in-loco** para a versão de 64 bits do SQL Server 2012 com SP1|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **e** SQLServer2012SP1-FullSlipstream-x64-ENU.box [aqui](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  

### <a name="known-issues-fixed-in-this-service-pack"></a>Problemas conhecidos corrigidos neste service pack  
Para obter uma lista completa de bugs e problemas conhecidos corrigidos neste service pack, consulte [este artigo mestre da Base de Dados de Conhecimento](http://support.microsoft.com/kb/2674319).   

### <a name="reinstalling--instances-of-sql-server-failover-cluster-fails-if-you-use-the-same-ip-address"></a>A reinstalação de instâncias do Cluster de Failover do SQL Server falha qando o mesmo endereço IP é usado  
**Problema:** se você especificar um endereço IP incorreto durante uma instalação da instância do cluster de failover do SQL Server, a instalação falhará. Depois que você desinstalar a instância com falha, e se tentar reinstalar a instância do cluster de failover do SQL Server com o mesmo nome de instância e o endereço de IP correto, a instalação falhará. A falha ocorre devido ao grupo de recursos duplicado por trás da instalação anterior.  
  
**Solução alternativa:** para resolver esse problema, use um nome de instância diferente durante a reinstalação, ou exclua manualmente o grupo de recursos antes de reinstalar. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server](http://msdn.microsoft.com/library/ms191545). 
  
### <a name="analysis-services-and-powerpivot"></a>Analysis Services e PowerPivot  
  
##### <a name="powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>A ferramenta de configuração do PowerPivot não cria a Galeria do PowerPivot  
**Problema:** a Ferramenta de Configuração do PowerPivot provisiona um Site de Equipe e, portanto, a Galeria PowerPivot não é criada.  
  
**Solução alternativa:** crie um novo aplicativo (biblioteca).  
  
1.  Verifique se o recurso de coleção de sites **Integração de recursos do PowerPivot para coleções de sites** está ativo.  
  
2.  Na página **Conteúdo do site** de um site existente, clique em **adicionar aplicativo**.  
  
3.  Clique em **Galeria PowerPivot**.  
  
#### <a name="to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>Para usar o PowerPivot para Excel com o Excel 2013, você precisa usar o suplemento que é instalado com o Excel  
**Problema:** com o Office 2010, o PowerPivot para Excel é um suplemento independente baixado em [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx). Ele também pode ser baixado no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=29074). Observe que há duas versões do suplemento PowerPivot disponíveis como download: uma é fornecida com o SQL Server 2008 R2 e outra, com o SQL Server 2012. No entanto, para o Office 2013, o PowerPivot para Excel é fornecido com o Office e é instalado quando você instala o Excel. Embora as versões do SQL Server 2008 R2 e SQL Server 2012 do PowerPivot para Excel 2010 não sejam compatíveis com o Excel 2013, você ainda pode instalar o PowerPivot para Excel 2010 no computador cliente se quiser executar o Excel 2010 lado a lado com o Excel 2013. Em outras palavras, as duas versões do Excel podem coexistir, além dos suplementos correspondentes do PowerPivot.  
  
**Solução alternativa:** para usar o PowerPivot para Excel 2013, você deverá habilitar o suplemento do COM. No Excel 2013, selecione **Arquivo** | **Opções** | **Suplementos**. Na caixa suspensa **Gerenciar** , selecione **Suplementos do COM** e clique em **Ir**. Em **Suplementos do COM**, selecione **Microsoft Office PowerPivot para Excel 2013** e clique em **OK**.  
  
### <a name="reporting-services"></a>Reporting Services  
  
#### <a name="install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>Instalar e configurar o SharePoint Server 2013 antes de instalar o Reporting Services  
**Problema:** complete os seguintes requisitos **antes** de instalar o SQL Server Reporting Services (SSRS).  
  
1.  Execute a ferramenta de preparação dos produtos do SharePoint 2013.  
  
2.  Instale o SharePoint Server 2013.  
  
3.  Execute o Assistente de configuração de produto do SharePoint 2013 ou complete um conjunto equivalente de etapas de configuração para configurar o farm do SharePoint.  
  
**Solução alternativa:**  se você instalou o modo do SharePoint do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] antes de o farm do SharePoint ter sido configurado, a solução alternativa necessária dependerá de quais outros componentes estão instalados.  
  
#### <a name="power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>O Power View no SharePoint Server 2013 exige o Microsoft.AnalysisServices.SPClient.dll  
**Problema:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não instala um componente obrigatório, **Microsoft.AnalysisServices.SPClient.dll**. Se você instalar a Visualização do SharePoint Server 2013 e o [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint, mas não baixar e instalar o pacote do instalador do PowerPivot para SharePoint 2013, **spPowerPivot.msi** , o Power View não funcionará e exibirá os seguintes sintomas.  
  
**Sintomas:** quando você tenta criar um relatório do Power View, vê uma mensagem de erro semelhante à seguinte:  
  
-   "...Não é possível criar uma conexão com a fonte de dados...''  
  
Os detalhes de erro internos conterão uma mensagem semelhante à seguinte:  
  
-   "O valor 'SharePoint Principal' não tem suporte para a propriedade de cadeia de conexão 'Identidade do usuário'."  
  
**Solução alternativa:** instalar o pacote do instalador do PowerPivot para SharePoint 2013 (**spPowerPivot.msi**) no SharePoint Server 2013. O pacote do instalador está disponível como parte do feature pack do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] . O feature pack pode ser baixado do centro de download [!INCLUDE[msCoName](../includes/msconame-md.md)] em [SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)  
  
#### <a name="power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>As planilhas do Power View em uma pasta de trabalho do PowerPivot são excluídas depois de uma atualização de dados agendada  
**Problema**: no suplemento PowerPivot para SharePoint, o uso da **Atualização de Dados Agendada** em uma pasta de trabalho com o Power View irá excluir as planilhas do Power View.  
  
**Solução alternativa**: para usar a **Scheduled Data Refresh** com as pastas de trabalho do Power View, crie uma pasta de trabalho PowerPivot que seja apenas o modelo de dados. Crie uma pasta de trabalho separada com planilhas do Excel e do Power View que se vinculem à pasta de trabalho PowerPivot com o modelo de dados. Apenas a pasta de trabalho PowerPivot com o modelo de dados deve ser agendada para atualização.  
  
### <a name="data-quality-services"></a>Data Quality Services  
  
#### <a name="dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>DQS disponível na edição incorreta do SQL Server 2012  
**Problema:** na versão RTM do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] , o recurso DQS (Data Quality Services) está disponível nas edições do SQL Server além das edições Enterprise, Business Intelligence e Developer. Depois de instalar o SQL Server 2012 SP1, o DQS não estará disponível em todas as edições exceto as edições Enterprise, Business Intelligence e Developer.  
  
**Solução alternativa**: se você estiver usando o DQS em uma edição sem suporte, atualize para uma edição com suporte ou remova a dependência desse recurso de seus aplicativos.  
  
### <a name="sql-server-express"></a>SQL Server Express  
  
#### <a name="full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>Versão completa do SQL Server Management Studio disponível no SQL Server 2012 Express SP1  
A versão do SQL Server 2012 Express Service Pack 1 (SP1) inclui a versão completa do SQL Server 2012 Management Studio (que anteriormente estava disponível no DVD do SQL Server 2012) em vez do SQL Server 2012 Management Studio Express. Para baixar e instalar o SQL Server 2012 Express SP1, consulte [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905).  
  
### <a name="change-data-capture-service-and-designer-for-oracle-by-attunity"></a>Serviço Change Data Capture e Designer para Oracle da Attunity  
  
#### <a name="upgrading-the-cdc-service-and-designer"></a>Atualizando o serviço CDC e Designer  
**Problema:** se o Change Data Capture Designer para Oracle e o Serviço Change Data Capture para Oracle da Attunity estiverem instalados no computador no momento em que você instalar o SQL Server 2012 SP1, esses componentes não serão atualizados instalando o SP1.  
  
**Solução alternativa:** atualizar os componentes CDC para a versão mais recente:  
  
1.  Baixar os arquivos .msi para o Serviço Change Data Capture para Oracle da Attunity na [página de download dos feature packs do SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266).  
  
2.  Execute o arquivo .msi.  
  
### <a name="sql-server-data-tier-application-framework-dacfx"></a>DACFx (SQL Server Data-Tier Application Framework)  
**Suporte à atualização in-loco**  
  
Esta versão da Estrutura de Aplicativo da Camada de Dados (DACFx) fornece suporte à atualização in-loco de versões anteriores. Portanto, não é necessário remover as instalações anteriores da DACFx antes de atualizar para esta versão. Você poderá encontrar futuras versões da DACFx [aqui](https://msdn.microsoft.com/library/dn702988.aspx).  
  
**Suporte a índice XML seletivo**  
  
O SQL Server 2012 SP1 inclui suporte a [Índice XML seletivo (SXI)](http://msdn.microsoft.com/598ecdcd-084b-4032-81b2-eed6ae9f5d44), um novo recurso do SQL Server que fornece uma nova forma de indexar os dados da coluna XML com desempenho e eficiência crescentes.  
  
Agora a DACFx fornece suporte a índices SXI em todos os cenários DAC e a todas as ferramentas de cliente. O SXI é compatível apenas com a versão mais recente das SSDT. As SSDT RTM e as versões de setembro de 2012 não são compatíveis com o SXI.  
  
**Suporte para formato de dados BCP nativo**  
  
Anteriormente, o formato de dados usado para armazenar os dados da tabela dentro dos pacotes DACPAC e BACPAC era JSON. Com esta atualização, o BCP nativo agora é o formato de persistência de dados. Essa alteração apresenta a fidelidade aprimorada do tipo de dados do SQL Server à DACFx, incluindo suporte para tipos SQL_Variant, assim como desempenho aprimorado de implantação de dados para bancos de dados em grande escala.  
  
**A preservação do estado Restrição CHECK na criação/implantação do pacote**  
  
Anteriormente, a DACFx não preservava o estado (WITH CHECK/NOCHECK) das Restrições CHECK definidas nas tabelas no esquema de banco de dados nem armazenava essas informações dentro de DACPACs. Esse comportamento poderia levar a problemas potenciais na implantação do pacote quando há dados de tabela existente que violam as Restrições CHECK. Com esta atualização, a DACFx agora armazena o estado atual das Restrições CHECK dentro de DACPAC quando extraídas de um banco de dados e restaura apropriadamente esse estado na implantação do pacote.  
  
**Atualizações da SqlPackage.exe (ferramenta de linha de comando da DACFx)**  
  
-   Extrair DACPAC com dados – Cria um arquivo de instantâneo de banco de dados (.dacpac) de um banco de dados dinâmico SQL Server ou SQL do Windows Azure que contém dados de tabelas de usuário além do esquema de banco de dados. Esses pacotes podem ser publicados em um banco de dados SQL Server ou SQL do Windows Azure existente ou novo, usando a ação Publicar da SqlPackage.exe. Os dados contidos no pacote substituem os dados existentes no banco de dados de destino.  
  
-   Exportar BACPAC – Cria um arquivo de backup lógico (.bacpac) de um banco de dados dinâmico SQL Server ou SQL do Windows Azure que contém o esquema de banco de dados e dados de usuário que podem ser usados para migrar um banco de dados SQL Server ou SQL do Windows Azure no local. Os bancos de dados compatíveis com o Azure podem ser exportados e importados posteriormente entre versões com suporte do SQL Server.  
  
-   Importar BACPAC – Importa um arquivo .bacpac para popular um banco de dados vazio ou criar um novo banco de dados SQL Server ou SQL do Windows Azure.  
  
A documentação completa da SqlPackage.exe no MSDN pode ser encontrada [aqui](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx).  
  
**Compatibilidade de pacote**  
  
Esta versão apresenta vários cenários de compatibilidade futura para os pacotes de DAC.  
  
-   Os pacotes de DAC criados por esta versão que não contêm dados de tabelas ou elementos SXI talvez possam ser utilizados por versões anteriores da DACFx (SQL Server 2012 RTM, SQL Server 2012 CU1 e DACFx de setembro de 2012).  
  
-   Todos os pacotes de DAC criados por versões anteriores da DACFx podem ser utilizados por esta versão.  
  
## <a name="see-also"></a>Consulte Também
- [Instalar as atualizações de manutenção do SQL Server 2012](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [Como identificar sua versão de SQL Server e edição](https://support.microsoft.com/help/321185)
- [Instalar as atualizações de manutenção do SQL Server 2012](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [Como identificar sua versão e edição do SQL Server ](https://support.microsoft.com/help/321185) 
- [Como determinar a versão e a edição do SQL Server](http://support.microsoft.com/kb/321185)  
- [Recursos com suporte nas edições do SQL Server 2014](http://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
