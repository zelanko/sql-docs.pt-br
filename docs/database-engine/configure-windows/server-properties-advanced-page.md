---
title: Propriedades do servidor (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.advanced.f1
ms.assetid: cc5e65c2-448e-4f37-9ad4-2dfb1cc84ebe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d7ae58695fabc363a432f21d91a70ccc3a3f4dc6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619504"
---
# <a name="server-properties---advanced-page"></a>Propriedades do servidor – página Avançado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para exibir ou modificar as configurações avançadas do servidor.  
  
 **Para exibir as páginas Propriedades do Servidor**  
  
-   [Exibir ou alterar as propriedades de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
## <a name="containment"></a>Containment  
 Habilitar bancos de dados independentes  
 Indica se esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite bancos de dados independentes. Quando definido como **True**, um banco de dados independente poderá ser criado, restaurado ou anexado. Quando definido como **False**, um banco de dados independente não pode ser criado, restaurado nem anexado a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Alterar a propriedade de contenção pode ter um impacto na segurança do banco de dados. Habilitar bancos de dados independentes permite que proprietários de banco de dados concedam acesso a esse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Desabilitar bancos de dados independentes pode impedir que os usuários se conectem. Para entender o impacto da propriedade de contenção, veja [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md) e [Práticas recomendadas de segurança com bancos de dados independentes](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="filestream"></a>FILESTREAM  
 **Nível de acesso FILESTREAM**  
 Mostra o nível de suporte de FILESTREAM atual configurado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para alterar o nível de acesso configurado, selecione um dos seguintes valores:  
  
 **Desabilitado**  
 Os dados BLOB (objeto grande binário) não podem ser armazenados em um sistema de arquivos. Este é o valor padrão.  
  
 **Acesso ao Transact-SQL habilitado**  
 Os dados de FILESTREAM podem ser acessados através do [!INCLUDE[tsql](../../includes/tsql-md.md)], mas não pelo sistema de arquivos.  
  
 **Acesso completo habilitado**  
 Os dados de FILESTREAM podem ser acessados através do [!INCLUDE[tsql](../../includes/tsql-md.md)] e pelo sistema de arquivos.  
  
 Ao habilitar o FILESTREAM pela primeira vez, talvez seja necessário reiniciar o computador para configurar os drivers.  
  
 **Nome do Compartilhamento de FILESTREAM**  
 Exibe o nome somente leitura do compartilhamento de FILESTREAM selecionado durante a instalação. Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
## <a name="miscellaneous"></a>Diversos  
 **Permitir que Gatilhos Disparem Outros Gatilhos**  
 Permite que gatilhos acionem outros gatilhos. Os gatilhos podem ser aninhados até no máximo 32 níveis. Para obter mais informações, confira a seção “Gatilhos aninhados” em [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 **Limite de Processo Bloqueado**  
 O limite, em segundos, no qual os relatórios de processos bloqueados são gerados. O limite pode ser definido de 0 a 86.400. Por padrão, não são produzidos relatórios de processo bloqueado. Para obter mais informações, veja [Opção blocked process threshold de configuração de servidor](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md).  
  
 **Limite do Cursor**  
 Especifique o número de linhas no conjunto de cursores em que os conjuntos de chaves de cursor são gerados de forma assíncrona. Quando os cursores geram um conjunto de chaves para um conjunto de resultados, o otimizador de consulta calcula o número de linhas que serão retornadas para aquele conjunto de resultados. Se o otimizador de consulta calcular que o número de linhas retornadas é maior do que esse limite, o cursor será gerado de forma assíncrona, permitindo que o usuário busque linhas do cursor enquanto o cursor continua sendo populado. Caso contrário, o cursor é gerado de forma síncrona e a consulta aguarda até que todas as linhas sejam retornadas.  
  
 Se definido como -1, todos os conjuntos de chaves serão gerados de forma síncrona. Isso beneficia conjuntos de cursores pequenos. Se definidos como 0, todos os conjuntos de chaves de cursor são gerados de forma assíncrona. Com outros valores, o otimizador de consulta compara o número de linhas previstas no conjunto de cursor e cria o conjunto de chaves de forma assíncrona se ele exceder o número definido. Para obter mais informações, veja [Configurar a opção cursor threshold de configuração de servidor](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md).  
  
 **Idioma de Texto Completo Padrão**  
 Especifica um idioma padrão para colunas indexadas de texto completo. A análise linguística dos dados indexados de texto completo depende do idioma dos dados. O valor padrão dessa opção é o idioma do servidor. Para obter a linguagem que corresponde à configuração exibida, veja [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
 **Idioma Padrão**  
 O idioma padrão para todos os novos logons, a menos que especificado de outra maneira.  
  
 **Opção de Atualização de Texto Completo**  
 Controla como são migrados índices de texto completo ao atualizar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Essa propriedade se aplica à atualização anexando um banco de dados, restaurando um backup do banco de dados, restaurando um backup de arquivo ou copiando o banco de dados usando o Assistente para Copiar Banco de Dados.  
  
 As alternativas são como segue:  
  
 **Importar**  
 Os catálogos de texto completo são importados. Essa operação é significativamente mais rápida que **Recriar**. No entanto, um catálogo de texto completo importado não usará os separadores de palavras novos e aprimorados introduzidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Sendo assim, no final, talvez você deseje recriar os catálogos de texto completo.  
  
 Se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recompilados. Essa opção está disponível apenas para bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 **Recompilar**  
 Os catálogos de texto completo são recompilados usando-se os separadores de palavras novos e aprimorados. A recompilação de índices pode demorar um pouco, e uma quantidade significativa de memória e CPU pode ser necessária após a atualização.  
  
 **Redefinir**  
 Os catálogos de texto completo são redefinidos. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] os arquivos de catálogos de texto completo são removidos, mas os metadados dos catálogos e dos índices de texto completo são preservados. Depois de serem atualizados, todos os índices de texto completo são desabilitados para o controle de alteração e os rastreamentos não são iniciados automaticamente. O catálogo permanecerá vazio até você executar uma população completa manualmente, depois que a atualização for concluída.  
  
 Para obter informações sobre como escolher a opção de atualização de texto completo, veja [Atualizar pesquisa de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
> [!NOTE]  
>  A opção de atualização de texto completo também pode ser definida com o uso da ação [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)upgrade_option.  
  
 Depois de anexar, restaurar ou copiar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados se torna logo disponível e, em seguida, é atualizado de forma automática. Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida como **Importar**, se não houver um catálogo de texto completo disponível, os índices de texto completo associados serão recompilados. Para obter informações sobre como exibir ou alterar a configuração da propriedade **Full-Text Upgrade Option** , veja [Gerenciar e monitorar a pesquisa de texto completo para uma instância de servidor](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
 **Tamanho Máximo da Replicação de Texto**  
 Especifica o tamanho máximo (em bytes) de dados dos tipos **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **xml**e **image** que podem ser adicionados a uma coluna replicada ou capturada em uma única instrução INSERT, UPDATE, WRITETEXT ou UPDATETEXT. A alteração da configuração entra em vigor imediatamente. Para obter mais informações, veja [Configurar a opção max text repl size de configuração de servidor](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md).  
  
 **Examinar Procedimentos de Inicialização**  
 Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examinará a execução automática de procedimentos armazenados na inicialização. Se definido como **True**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examina e executa todos os procedimentos armazenados executados automaticamente definidos no servidor. Se definido como **False** (o padrão), nenhum exame é executado. Para obter mais informações, veja [Configurar a opção scan for startup procs de configuração de servidor](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md).  
  
 **Corte de Ano de Dois Dígitos**  
 Indica o número de ano mais alto que pode ser digitado como um ano de dois dígitos. O ano listado e os 99 anos anteriores podem ser digitados como um ano de dois dígitos. Todos os outros anos devem ser digitados como um ano de quatro dígitos.  
  
 Por exemplo, a configuração padrão de 2049 indica que a data digitada como ‘14/3/49’ será interpretada como 14 de março de 2049 e a data digitada como ‘14/3/50’ será interpretada como 14 de março de 1950. Para saber mais, veja [Configurar a opção two digit year cutoff de configuração de servidor](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="network"></a>Rede  
 **Tamanho do Pacote de Rede**  
 Define o tamanho do pacote (em bytes) usado pela rede inteira. O tamanho do pacote padrão é de 4096 bytes. Se um aplicativo fizer operações de cópia em massa ou enviar ou receber quantias grandes quantidades de dados **text** ou **image** , um tamanho do pacote maior que o padrão poderá melhorar a eficiência, porque resulta em menos operações de leitura e gravação em rede. Se um aplicativo enviar e receber pequenas quantidades de informações, você pode definir o tamanho do pacote como 512 bytes, o que é suficiente para a maioria das transferências de dados. Para obter mais informações, veja [Configurar a opção network packet size de configuração de servidor](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md).  
  
> [!NOTE]  
>  Não altere o tamanho do pacote a menos que você tenha certeza que melhorará o desempenho. Para a maioria dos aplicativos, o tamanho do pacote padrão é o melhor.  
  
 **Tempo Limite de Logon Remoto**  
 Especifica o número de segundo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera antes de voltar de uma falha na tentativa de logon remoto. Essa configuração afeta conexões com provedores OLE DB estabelecidas para consultas heterogêneas. O valor padrão é 20 segundos. Um valor 0 permite uma espera infinita. Para obter mais informações, veja [Configurar a opção remote login timeout de configuração de servidor](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md).  
  
 A alteração da configuração entra em vigor imediatamente.  
  
## <a name="parallelism"></a>Paralelismo:  
 **Limite de Custo Para Paralelismo**  
 Especifica o limite sobre o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria e executa planos paralelos para consultas. O custo faz referência a um tempo decorrido estimado em segundos, exigido para a execução do plano serial em uma configuração de hardware específica. Só defina esta opção em multiprocessadores simétricos. Para obter mais informações, veja [Configurar a opção cost threshold for parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md).  
  
 **Locks**  
 Define o número máximo de bloqueios disponíveis, limitando assim a quantidade de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para eles. A configuração padrão é 0, a qual permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aloque e desaloque os bloqueios de forma dinâmica, baseado nas alterações de requisitos do sistema.  
  
 Recomenda-se permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use bloqueios dinamicamente. Para obter mais informações, veja [Configurar a opção locks de configuração de servidor](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md).  
  
 **Grau Máximo de Paralelismo**  
 Limita o número de processadores (até um máximo de 64) a serem usados na execução do plano paralelo. O valor padrão 0 usa todos os processadores disponíveis. Um valor de 1 suprime geração de planos paralelos. Um número maior do que 1 restringe o número máximo de processadores usados por uma única execução de consulta. Se um valor maior do que o número de processadores disponíveis for especificado, o número real de processadores disponíveis será usado. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
 **Espera da Consulta**  
 Especifica o tempo em segundos (de 0 a 2147483647) que uma consulta espera por recursos antes de acusar tempo limite. Se o valor padrão -1 for usado, o tempo limite será calculado como 25 vezes o custo estimado da consulta. Para obter mais informações, veja [Configurar a opção query wait de configuração de servidor](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
