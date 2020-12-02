---
title: Aplicativos de backup do SQL Server – VSS (Serviço de Cópias de Sombra de Volume) e Gravador do SQL
description: Descreve o componente Gravador do SQL e a função dele no processo de criação e restauração de instantâneos do VSS para bancos de dados do SQL Server.
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3f098dc361d4e30a82dee198bb8203d19b412613
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125437"
---
# <a name="sql-server-back-up-applications---volume-shadow-copy-service-vss-and-sql-writer"></a>Aplicativos de backup do SQL Server – VSS (Serviço de Cópias de Sombra de Volume) e Gravador do SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

O SQL Server fornece suporte para o VSS (Serviço de Cópias de Sombra de Volume) fornecendo um gravador (o Gravador do SQL), de modo que um aplicativo de backup de terceiros possa usar a estrutura VSS para fazer backup de arquivos de banco de dados. Este documento descreve o componente Gravador do SQL e a função dele no processo de criação e restauração de instantâneos do VSS para bancos de dados do SQL Server. Também captura detalhes de como configurar e usar o Gravador do SQL para trabalhar com aplicativos de backup na estrutura VSS.


## <a name="introduction"></a>Introdução

O SQL Server fornece suporte para a criação de instantâneos de dados do SQL Server com o VSS (Serviço de Cópias de Sombra de Volume). Isso é feito com o fornecimento de um gravador em conformidade com o VSS (o Gravador do SQL), de modo que um aplicativo de backup de terceiros possa usar a estrutura VSS para fazer backup de arquivos de banco de dados. Este documento descreve o componente Gravador do SQL e a função dele no processo de criação e restauração de instantâneos do VSS para bancos de dados do SQL Server. Também captura detalhes de como configurar e usar o Gravador do SQL para trabalhar com aplicativos de backup no contexto da estrutura VSS.

## <a name="definition-of-terms"></a>Definições de termos

- **Interface de Dispositivo Virtual**: o SQL Server fornece uma interface de programação de aplicativo chamada VDI (Interface de Dispositivo Virtual) que ajuda os fornecedores de software independentes a integrarem o SQL Server aos produtos, fornecendo suporte para operações de backup e restauração. Essas APIs foram projetadas para fornecer confiabilidade e desempenho máximos e dão suporte à gama completa de funcionalidades de backup e restauração do SQL Server, incluindo a gama completa de funcionalidades de backup dinâmico e de instantâneo. Para obter mais informações, confira [Especificação da Interface de Dispositivo de Backup Virtual do SQL Server 2005](https://www.microsoft.com/download/details.aspx?id=17282). 

- **Solicitante**: um processo (automatizado ou GUI) que solicita que um ou mais conjuntos de instantâneos sejam tirados de um ou mais volumes originais. Neste documento, um solicitante também é usado para implicar um aplicativo de backup que está criando um instantâneo de bancos de dados do SQL Server.

## <a name="about-vss"></a>Sobre o VSS

O VSS fornece a infraestrutura do sistema para executar aplicativos VSS em sistemas Windows. Embora seja amplamente transparente para o usuário e o desenvolvedor, o VSS faz o seguinte:

- Coordena as atividades de provedores, gravadores e solicitantes na criação e no uso de cópias de sombra.
- Fornece o provedor do sistema padrão.
- Implementa a funcionalidade de driver de baixo nível necessária para o funcionamento de qualquer provedor.

O serviço VSS é iniciado sob demanda; portanto, para que as operações do VSS sejam bem-sucedidas, esse serviço precisa ser habilitado.

## <a name="vss-components"></a>Componentes do VSS

O VSS coordena as atividades dos seguintes componentes de cooperação: 

- Os provedores são os proprietários dos dados de cópia de sombra e criam uma instância das cópias de sombra.
- Os gravadores são aplicativos que alteram dados e participam do processo de sincronização da cópia de sombra.
- Os solicitantes iniciam a criação e a destruição das cópias de sombra. Nosso design se concentra no cenário em que o solicitante é um aplicativo de backup.

O VSS fornece coordenação entre estas partes: 

![Diagrama que mostra como o VSS fornece coordenação entre essas partes.](media/sql-server-vss-writer-backup-guide/coordinations.png)

Este diagrama mostra todos os componentes que participam de uma atividade típica de instantâneo do VSS. Nesse cenário, o SQL Server (incluindo o Gravador do SQL) funciona como um gravador em uma das caixas do Gravador.  Outros gravadores desse tipo podem ser o Exchange Server etc.

No restante deste documento, pressupõe-se que o leitor esteja familiarizado com os termos da estrutura VSS.  Confira a documentação sobre o [Serviço de Cópias de Sombra de Volume](/windows/win32/vss/volume-shadow-copy-service-overview) para obter detalhes.

## <a name="about-sql-writer"></a>Sobre o Gravador do SQL

O Gravador do SQL é um gravador VSS fornecido pelo SQL Server. Ele cuida da interação do VSS com o SQL Server. O Gravador do SQL é fornecido com o SQL Server como um serviço autônomo e é instalado como parte da instalação do SQL Server. Por padrão, o Gravador do SQL não está habilitado. Ele precisa ser explicitamente habilitado para ser executado no computador do servidor.

A função do Gravador do SQL em uma operação de backup de instantâneo do VSS: 

![Instantâneo do VSS](media/sql-server-vss-writer-backup-guide/sql-vss-snapshot.png)



## <a name="configuring-the-sql-writer"></a>Como configurar o Gravador do SQL

O Serviço Gravador do SQL é instalado no sistema como parte da instalação do SQL Server e é configurado para ser iniciado automaticamente quando o Windows é iniciado. 

### <a name="sql-writer-service-account"></a>Conta do Serviço Gravador do SQL

Durante a instalação, a conta do Gravador do SQL será instalada para usar a conta Sistema Local. Como o Gravador do SQL precisa se comunicar com o SQL Server usando APIs exclusivas da VDI, a conta do Gravador do SQL precisa ter direitos de acesso suficientes para o SQL Server e o VSS.  A configuração do serviço como uma conta Sistema Local fornece direitos suficientes para que o serviço seja executado corretamente.

  > [!NOTE]
  > Para que o Serviço Gravador do SQL funcione corretamente, é importante garantir que a conta Sistema Local não seja removida da função 'sa' da instância do SQL Server.

### <a name="enabling-and-starting-sql-writer"></a>Como habilitar e iniciar o Gravador do SQL

Para iniciar e usar o Gravador do SQL, é necessário fazer o seguinte:

O Serviço Gravador do SQL pode ser habilitado pela marcação desse serviço como "Automático". Para abrir os serviços por meio do painel de controle, clique em Iniciar, clique em Painel de Controle, clique duas vezes em Ferramentas Administrativas e, em seguida, clique duas vezes em Serviços. No painel Serviços, clique duas vezes no Serviço Gravador do SQL e modifique a propriedade "Tipo de Inicialização" como "Automático".

O serviço também deve ser iniciado pela seleção do botão "Iniciar" na propriedade "Status do Serviço" na tela da propriedade do serviço mencionada acima.

Para sua conveniência, o Serviço Gravador do SQL fará essas alterações automaticamente na primeira vez em que for iniciado.

  > [!NOTE]
  > Em alguns casos em que uma instância do SQL Server Express está instalada e um aplicativo está usando o recurso Instâncias de Usuário, o Gravador do SQL pode ser iniciado automaticamente pelo SQL Server. Isso é feito para facilitar a enumeração dessas Instâncias de Usuário durante uma operação de backup do VSS. 

## <a name="backuprestore-operations-and-supported-versions"></a>Operações de backup/restauração e versões compatíveis

### <a name="version-support"></a>Suporte da versão

O Gravador do SQL é enviado como parte do SQL Server e só dá suporte às instâncias do SQL Server. 

O Gravador do SQL também vai enumerar as instâncias do SQL Server Express. As instâncias de usuário iniciadas pelo SQL Server Express também serão enumeradas pelo Gravador do SQL.


## <a name="supported-backuprestore-operations"></a>Operações de backup/restauração compatíveis

O SQL Server (com o Gravador do SQL) dará suporte aos seguintes modos de operações de backup baseadas no VSS:

- Não baseados em componentes
- Baseados em componentes

### <a name="noncomponent-based-backup-operations"></a>Operações de backup não baseadas em componentes

Os backups não baseados em componentes selecionam bancos de dados implicitamente usando a lista de volumes no conjunto de instantâneos. O Gravador do SQL verifica se há bancos de dados subdivididos que geram um erro, se encontrado. Um banco de dados subdividido é aquele em que um subconjunto de arquivos é selecionado pela lista de volumes.

No modelo não baseado em componentes, só há suporte para os bancos de dados com o modelo de recuperação simples. Não há suporte para roll forward após uma restauração.

### <a name="component-based-backup-operations"></a>Operações de backup baseadas em componentes

Os backups baseados em componentes são preferenciais e recomendados com o Gravador do SQL, pois o aplicativo (aplicativo de backup do VSS) selecionará explicitamente os bancos de dados dos metadados que são retornados do Gravador do SQL. O conjunto de instantâneos deve incluir todos os volumes necessários para fazer backup desses bancos de dados. A infraestrutura do VSS não adiciona automaticamente os volumes necessários ao conjunto selecionado de bancos de dados. Todos os volumes de backup devem ser incluídos no conjunto de instantâneos de volume. É responsabilidade do aplicativo de backup garantir que todos os volumes de backup sejam incluídos no conjunto de instantâneos.  O Gravador do SQL detectará bancos de dados subdivididos (com volumes de backup fora do conjunto de instantâneos) e falhará o backup.

O restante deste tópico pressupõe que os backups baseados em componentes sejam usados como parte do processo de criação de instantâneo do VSS para o SQL Server.

## <a name="features-supported-by-sql-writer"></a>Recursos compatíveis com o Gravador do SQL


- **Texto completo**: o Gravador do SQL relata os contêineres de catálogo de texto completo com especificações de arquivo recursivo nos componentes de banco de dados no documento de metadados do gravador.  Eles são incluídos automaticamente no backup quando o componente de banco de dados é selecionado
- **Backup/restauração diferenciais**: o Gravador do SQL dá suporte a backup/restauração diferenciais por meio de dois mecanismos diferenciais do VSS: Arquivo parcial e arquivo diferenciado pela hora da última modificação.
- **Arquivo Parcial**:   o Gravador do SQL usa o mecanismo de Arquivo Parcial do VSS para relatar os intervalos de bytes alterados nos arquivos de banco de dados.  
- **Arquivo Diferenciado pela Hora da Última Modificação**: o Gravador do SQL usa o mecanismo Arquivo Diferenciado pela Hora da Última Modificação do VSS para relatar os arquivos alterados em catálogos de texto completo.
- **Restauração com movimentação**: o Gravador do SQL dá suporte à especificação de Novo Destino do VSS durante a restauração.  A especificação de Novo Destino do VSS permite que um arquivo de log/banco de dados ou um contêiner de catálogo de texto completo seja realocado como parte da operação de restauração.
- **Renomeação de banco de dados**: um solicitante poderá precisar restaurar um Banco de Dados SQL com um novo nome, especialmente se o banco de dados for restaurado lado a lado com o banco de dados original. O Gravador do SQL dá suporte à renomeação de um banco de dados durante a operação de restauração, desde que o banco de dados permaneça dentro da instância original do SQL.
- **Backup somente cópia**: às vezes, é necessário fazer um backup destinado a uma finalidade especial, por exemplo, quando você precisa fazer uma cópia de um banco de dados para fins de teste.  Esse backup não deve afetar os procedimentos gerais de backup e restauração do banco de dados. O uso da opção COPY_ONLY especifica que o backup é feito "fora de banda" e não deve afetar a sequência normal de backups. O Gravador do SQL dá suporte ao tipo de backup "somente cópia" com instâncias do SQL Server.
- **Recuperação automática de instantâneo do banco de dados**:   normalmente, um instantâneo de um banco de dados do SQL Server obtido com a estrutura VSS está em um estado não recuperado. Os dados no instantâneo não podem ser acessados com segurança antes de passarem pela fase de recuperação para reverter as transações em andamento e colocar o banco de dados em um estado consistente. É possível que um aplicativo de backup do VSS solicite a recuperação automática dos instantâneos, como parte do processo de criação de instantâneo.

Esses novos recursos e o uso deles são descritos mais detalhadamente em Detalhes da opção de backup e restauração neste tópico.

### <a name="what-is-not-supported"></a>O que não tem suporte

- Não há suporte para backups de log no Gravador do SQL.
- Não há suporte para backups de arquivos/grupos de arquivos.
- Não há suporte para restauração de página.
- Não há suporte para instantâneos de banco de dados. Eles são ignorados durante a criação de instantâneos do VSS de componentes e de não componentes. 
- Bancos de dados de fechamento automático ou bancos de dados com o desligamento habilitado.
- O Linux não fornece uma estrutura VSS e, portanto, o Gravador do SQL não está disponível no Linux

A tabela a seguir lista os tipos de backups de instantâneo compatíveis com o Gravador do SQL/o SQL Server trabalhando com a estrutura VSS para todas as edições do SQL Server.

| **Operação de backup/restauração**                 | **Baseados em componentes**           | **Não baseados em componentes** |
|:-------------------------------------------- | :---------------------------- | :--------------------- |
|Backup de dados completo </br> (Incluindo o catálogo de texto completo)| Sim                     | Sim                    |
|Restauração completa                                  | Sim                           | Sim                    |
|Restauração completa (sem recuperação)                    | Sim                           | Não                     |
|Backup Diferencial                           | Sim                           | Não                     |
|Restauração diferencial                          | Sim                           | Não                     |
|Restauração com movimentação                             | Sim                           | Não                     |
|Renomeação de banco de dados                               | Sim                           | Não                     |
|Copiar Somente Backup                              | Sim                           | Não                     |
|Instantâneos recuperados automaticamente                       | Sim                           | Não                     |
|Backup de Log                                    | Não                            | Não                     |
|Instantâneos de banco de dados                            | Não                            | Não                     |
|Bancos de dados de fechamento automático</br> Bancos de dados com desligamento | Sim                        | Não                     |
|Bancos de dados do grupo de disponibilidade                  | Sim                           | Não no secundário        | 




## <a name="snapshot-creation-process"></a>Processo de criação de instantâneo

A estrutura VSS coordena as atividades de um solicitante (um aplicativo de backup) e o Gravador do SQL durante a criação de instantâneos do SQL Server. Para habilitar essa coordenação, a estrutura VSS define as interfaces do solicitante e do gravador.  Essas interfaces devem ser implementadas pelos aplicativos solicitantes e pelos gravadores participantes. O Gravador do SQL implementa as interfaces de gravador necessárias. Como parte do processo de criação de instantâneo, as interfaces do Gravador do SQL são chamadas pela estrutura VSS. O Gravador do SQL interage com as instâncias do SQL Server no sistema para facilitar a criação de instantâneos.

A estrutura VSS define um conjunto de APIs para uso de um aplicativo solicitante/de backup. Um desenvolvedor de aplicativos de backup precisa seguir esses padrões de chamada à API para trabalhar com o processo de criação de instantâneo da estrutura VSS. As seções a seguir descrevem o processo de criação de instantâneo do ponto de vista do Gravador do SQL. Elas também fornecem detalhes de algumas das interações internas entre o solicitante, a estrutura VSS, o Gravador do SQL e as instâncias do SQL Server. Para obter mais informações sobre essas etapas e os detalhes das interfaces da estrutura VSS, confira a documentação sobre o Serviço de Cópias de Sombra de Volume.    

  > [!NOTE]
  > Pressupõe-se que o leitor esteja familiarizado com a estrutura VSS e o processo de criação de backup em geral. Essas seções são fornecidas como informações suplementares sobre como o Gravador do SQL participa do processo de criação de backup do VSS.

## <a name="snapshot-creation-workflow"></a>Fluxo de trabalho de criação de instantâneo

![Fluxo de dados](media/sql-server-vss-writer-backup-guide/dataflow-chart.png)

A imagem mostra o diagrama de fluxo de dados durante uma operação de backup/criação de instantâneo baseada em componentes. Para entender com mais detalhes as tarefas básicas envolvidas na execução de um backup, é útil dividir esta visão geral nas seguintes fases:

- Inicialização do backup
- Fase de descoberta do backup
- Tarefas pré-backup
- Backup real dos arquivos
- Término do backup



### <a name="backup-initialization"></a>Inicialização do backup

Durante essa fase do backup, o solicitante (aplicativo de backup) é associado à interface do instantâneo **IvssBackupComponents** e o inicializa em preparação para o backup. Ele também chama a API do VSS **IVssGatherWriterMetadata** para instruir a estrutura VSS a coletar metadados de todos os gravadores.

A estrutura VSS chamará cada um dos gravadores registrados, incluindo o Gravador do SQL para os metadados do gravador usando o evento **OnIdentify**. O Gravador do SQL consultará as instâncias do SQL Server para obter as informações de metadados de backup de cada banco de dados e criar o Documento de Metadados do Gravador. Essa fase também é conhecida como enumeração de metadados.

O Documento de Metadados do Gravador é um documento que contém informações transmitidas do gravador para o solicitante (aplicativo de backup). O Documento de Metadados do Gravador contém as seguintes informações:

- A ID do aplicativo e o nome amigável.
- Em que local há arquivos e componentes.
- Quais arquivos precisam ser incluídos e excluídos em um backup.
- Quais opções devem ser usadas no momento da restauração.
- Isso é transmitido novamente para o solicitante por meio da estrutura VSS.

### <a name="sql-writer-metadata-document"></a>Documento de metadados do Gravador do SQL

Este é um documento XML criado por um gravador (o Gravador do SQL, nesse caso) usando a interface **IVssCreateWriterMetadata** e que contém informações sobre o estado e os componentes do gravador. Os detalhes estruturais de um Documento de Metadados do Gravador são descritos na documentação da API do VSS. Estes são alguns dos detalhes do Documento de Metadados do Gravador do SQL.

- Informações de identificação do gravador
    - **Nome do gravador** – L"SqlServerWriter"
    - **ID da classe do gravador** – 0xa65faa63, 0x5ea8, 0x4ebc, 0x9d, 0xbd, 0xa0, 0xc4, 0xdb, 0x26, 0x91, 0x2a 
    - **ID da instância do gravador** – L"SQL Server:SQLWriter" 
    - **VSSUsageType** – VSS_UT_USERDATA 
    - **VSSSourceType** – VSS_ST_TRANSACTEDDB 
- Informações no nível do gravador – VSS_APP_BACK_END 
- Especificação do método de restauração – VSS_RME_RESTORE_IF_CAN_REPLACE.
- Esquema de backup compatível (API IVssCreateWriterMetadata::SetBackupSchema)
    - VSS_BS_DIFFERENTIAL – backup diferencial
    - VSS_BS_TIMESTAMPED – baseado em carimbo de data/hora: para arquivos de catálogo de texto completo.
    - VSS_BS_LAST_MODIFY – backup diferencial baseado na hora da última modificação.
    - VSS_BS_WRITER_SUPPORTS_NEW_TARGET – dá suporte à opção de localização de novo destino.
    - VSS_BS_WRITER_SUPPORTS_RESTORE_WITH_MOVE – dá suporte à restauração "com movimentação"
    - VSS_BS_COPY – dá suporte à opção de backup "somente cópia".
- Informações no nível do componente – contém informações específicas no nível do componente fornecidas pelo Gravador do SQL.
   - **Tipo** – VSS_CT_FILEGROUP
   - **Nome** – nome do componente (nome do banco de dados)
   - **Caminho lógico** – da instância do servidor (estará no formato "servidor\nome-da-instância" para as instâncias nomeadas e "servidor" para a instância padrão.)
   - **Sinalizadores de componentes**
   - **VSS_CF_APP_ROLLBACK_RECOVERY** – indica que os instantâneos do SQL Server sempre exigem uma fase de "recuperação" para tornar os arquivos consistentes e utilizáveis para cenários de não backup (ou seja, reversão de aplicativo).
   - Selecionável – verdadeiro
   - Selecionável para restauração – verdadeiro 
   - Métodos de restauração compatíveis – VSS_RME_RESTORE_IF_CAN_REPLACE

A única extensão da estrutura do conjunto de componentes no SQL Server é a introdução de catálogos de texto completo.  Catálogos de texto completo são diretórios de contêineres, que não podem ser expressos como arquivos de log nem de banco de dados do VSS, considerando que os arquivos de log e de banco de dados do VSS não têm especificação recursiva.  Portanto, o Gravador do SQL usará um componente de grupo de arquivos do VSS (VSS_CT_FILEGROUP) visando representar o componente no nível do banco de dados e os arquivos de grupo de arquivos para representar os arquivos de banco de dados, de log e do catálogo de texto completo.

Um exemplo de Documento de Metadados do Gravador é fornecido no final deste documento.

### <a name="backup-discovery"></a>Descoberta de backup
Nesta fase, um solicitante examina o Documento de Metadados do Gravador e cria e preenche um **Documento de Componente de Backup** com cada componente que precisa ser copiado em backup. Ele também especifica as opções de backup e os parâmetros necessários como parte desse documento. Para o Gravador do SQL, cada instância do banco de dados que precisa ser copiada em backup é um componente separado.

#### <a name="backup-components-document"></a>Documento de componentes de backup
Este é um documento XML criado por um solicitante (com a interface **IVssBackupComponents**) no decorrer da configuração de uma operação de restauração ou backup. O Documento de Componentes de Backup contém uma lista dos componentes explicitamente incluídos, de um ou mais gravadores, que participam de uma operação de backup ou restauração. Ele não contém informações de componentes implicitamente incluídos. Por outro lado, um Documento de Metadados do Gravador contém somente os componentes do gravador que podem participar de um backup. Os detalhes estruturais de um documento de componente de backup são descritos na documentação da API do VSS.

#### <a name="prebackup-tasks"></a>Tarefas pré-backup
As tarefas pré-backup no VSS concentram-se na criação de uma cópia de sombra dos volumes que contêm dados para backup. O aplicativo de backup salvará os dados da cópia de sombra, não do volume real.

Os solicitantes normalmente esperam os gravadores durante a preparação para o backup e enquanto a cópia de sombra está sendo criada. Se o Gravador do SQL estiver participando da operação de backup, ele precisará configurar os arquivos e também estar pronto para o backup e a cópia de sombra.

#### <a name="prepare-for-backup"></a>Preparação do backup
O solicitante precisará definir o tipo de operação de backup que precisa ser executado (**IVssBackupComponents::SetBackupState**) e, em seguida, notificar os gravadores por meio do VSS, a fim de se preparar para uma operação de backup usando **IVssBackupComponents::PrepareForBackup**.

O Gravador do SQL recebe acesso ao Documento de Componente de Backup, que fornece detalhes de quais bancos de dados precisam ser copiados em backup. Todos os volumes de backup devem ser incluídos no conjunto de instantâneos de volume. O Gravador do SQL detectará os bancos de dados subdivididos (com volumes de backup fora do conjunto de instantâneos) e falhará o backup durante o evento PostSnapshot.

**Iniciar instantâneo**. O solicitante iniciará o processo de instantâneo chamando a interface DoSnapshotSet da estrutura VSS.

**Criar instantâneo**. Esta fase envolve uma série de interações entre a estrutura VSS e o Gravador do SQL.

1. _Preparar instantâneo_. O Gravador do SQL chamará o SQL Server para se preparar para a criação do instantâneo.
1. _Congelar_. O Gravador do SQL chamará o SQL Server para congelar todas as E/Ss do banco de dados de cada um dos bancos dos dados cujo backup está sendo feito no instantâneo. Depois que o evento de congelamento retornar à estrutura VSS, o VSS criará o instantâneo.
1. _Descongelamento_. Nesse evento, o Gravador do SQL chamará as instâncias do SQL Server para "descongelar" ou retomar as operações normais de E/S.


A fase de criação de instantâneo é rápida (menos de 60 segundos), para impedir o bloqueio de todas as gravações no banco de dados.

**Pós-instantâneo** Se a recuperação automática for necessária para o instantâneo, o Gravador do SQL fará a recuperação automática de cada banco de dados selecionado para estar no instantâneo. Para obter uma explicação detalhada, confira Instantâneos recuperados automaticamente.

#### <a name="actual-backup-of-files"></a>Backup real dos arquivos

Nesta fase, o solicitante pode mover os dados para uma mídia de backup, se necessário. As interações nessa fase ocorrem entre o solicitante e a estrutura VSS. O Gravador do SQL não está envolvido.

1. Obter o status do gravador. Retorna o status dos gravadores. O solicitante poderá precisar resolver qualquer falha aqui.
1. Fazer o backup.

O solicitante pode mover os dados para uma mídia de backup, se necessário no momento.

#### <a name="backup-complete"></a>Backup concluído

Esse evento indicará que o backup foi concluído com êxito.

Esse também é o momento em que o Gravador do SQL pode confirmar o backup como uma base diferencial, se o backup atual é um backup completo do banco de dados (e não um backup somente cópia).


  > [!NOTE]
  > O solicitante deve enviar esse evento (evento de Backup Concluído) explicitamente para permitir que o Gravador do SQL confirme os backups de base diferenciais. Se esse evento não for recebido, o backup criado não será um backup de "base diferencial" qualificado.

#### <a name="save-writer-metadata"></a>Salvar metadados do gravador

O solicitante deve salvar o Documento de Componente de Backup e os metadados de backup de todos os componentes junto com os dados de backup do instantâneo. Esses metadados do gravador são necessários para o Gravador do SQL/o SQL Server em operações de restauração.

#### <a name="backup-termination"></a>Término do backup

O solicitante encerra a cópia de sombra liberando a interface **IVssBackupComponents** ou chamando **IVssBackupComponents::DeleteSnapshots**.

## <a name="restore-process"></a>Processo de restauração

Esta seção descreve o fluxo de trabalho da operação de restauração e as várias etapas envolvidas.

### <a name="restore-operation-workflow"></a>Fluxo de trabalho da operação de restauração

A figura a seguir mostra o diagrama de fluxo de dados durante uma operação de restauração do VSS. Para entender com mais detalhes as tarefas básicas envolvidas na execução de uma restauração, é útil dividir esta visão geral nos seguintes tópicos:

- Inicialização da restauração
- Preparação da restauração
- Restauração real dos arquivos
- Limpeza e término da restauração

![Fluxo do processo de restauração](media/sql-server-vss-writer-backup-guide/restore-process-flow.png)

Em todos os cenários de restauração baseada em componentes do VSS, a restauração de banco de dados é processada pelo Gravador do SQL em duas fases distintas.

- **Pré-restauração**:  o Gravador do SQL processa a validação, o fechamento de identificadores de arquivo etc.
- **Pós-restauração**:  o Gravador do SQL anexa o banco de dados e realiza a recuperação de pane, se necessário.

Entre essas duas fases, o aplicativo de backup é responsável por mover os dados relevantes abaixo do SQL.

### <a name="restore-initialization"></a>Inicialização da restauração

Durante a fase de inicialização de uma restauração, o solicitante precisa ter acesso aos Documentos de Componentes de Backup armazenados.

O Documento de Componente de Backup gerado durante a operação de backup é armazenado como parte dos dados de backup. O aplicativo de backup precisa transmitir esses dados novamente para a estrutura VSS. O Gravador do SQL obtém acesso a esses dados no início do processo de restauração.

#### <a name="prepare-for-restore"></a>Preparação da restauração

Ao preparar uma restauração, um solicitante usa o Documento Componentes de Backup armazenado para determinar o que será restaurado e como.  O solicitante selecionará os componentes a serem restaurados e definirá as opções de restauração apropriadas, conforme necessário.

Se um aplicativo de backup pretende aplicar backups diferenciais ou de log à operação de restauração atual (ou seja, a "Restauração sem recuperação" é necessária), a opção a seguir deverá ser definida como parte da criação do componente para cada banco de dados que está sendo restaurado.

```
IVssBackupComponents::SetAdditionalRestores(true)
```

Depois que todos os detalhes necessários forem definidos no Documento de Componente de Backup, o solicitante fará a chamada a **IVssBackupComponents::PreRestore** para gerar um evento PreRestore por meio do VSS que será processado pelos gravadores.

O Gravador do SQL examinará o Documento de Componente de Backup fornecido para identificar os bancos de dados apropriados, excluindo todos os arquivos adicionais criados desde o momento do backup. Ele também verifica os espaços em disco e fecha os identificadores de arquivo de banco de dados abertos, de modo que o solicitante possa copiar os dados necessários durante a fase de restauração. Essa fase permite que qualquer condição de erro antecipada seja detectada antes que o solicitante faça a cópia real dos arquivos. O SQL Server também colocará o banco de dados no estado de restauração.  Desse ponto em diante, o banco de dados não poderá ser iniciado até uma restauração bem-sucedida.

#### <a name="restore-files"></a>Restaurar arquivos

Essa é meramente uma ação específica do solicitante. É responsabilidade do solicitante (aplicativo de backup) copiar os arquivos de banco de dados necessários (ou copiar os intervalos relevantes de restaurações diferenciais) para os locais apropriados. O Gravador do SQL não está envolvido nesta operação.

#### <a name="cleanup-and-termination"></a>Limpeza e término

Depois que todos os dados forem restaurados nos locais corretos, uma chamada de um solicitante notificando que a operação de restauração foi concluída (**IvssBackupComponents::PostRestore**) permitirá que o Gravador do SQL saiba que as ações pós-restauração podem ser iniciadas.  O Gravador do SQL neste ponto executará a fase de restauração da recuperação de pane. Se a recuperação não for solicitada, ou seja, SetAdditionalRestores(true) não for especificado pelo solicitante, a fase desfazer da etapa de recuperação também será executada durante essa fase.

## <a name="backup-and-restore-option-details"></a>Detalhes da opção de backup e restauração

Esta seção descreve detalhadamente todas as opções de backup e restauração compatíveis com o Gravador do SQL.

### <a name="requestor-creates-a-volume-shadow-copy"></a>O solicitante cria uma cópia de sombra de volume

O Gravador do SQL pode estar envolvido no processo de criação de cópias de sombra de volume (fora do contexto de backup/restauração), porque os volumes de backup dos arquivos de BD foram adicionados ao conjunto de instantâneos de volume.  Nesse caso, o Gravador do SQL participa apenas da enumeração de metadados e da coordenação do congelamento, do descongelamento, de PrepareForSnapshot e PostSnapshot (confira o diagrama de fluxo de dados para obter detalhes).

### <a name="full-backuprestore"></a>Backup/restauração completos

O Gravador do SQL dá suporte a operações de backup/restauração completos nos modos baseados em componentes e não baseados em componentes.

### <a name="noncomponent-based-backup-and-restore"></a>Backup e restauração não baseados em componentes

Em um backup/restauração não baseado em componentes, o solicitante especifica um volume ou uma árvore de pastas para backup/restauração. Todos os dados na pasta/no volume especificado são copiados em backup/restaurados.

#### <a name="backup"></a>Backup

Em um backup não baseado em componentes, o Gravador do SQL seleciona os bancos de dados implicitamente usando a lista de volumes no conjunto de instantâneos.  O gravador verifica se há bancos de dados subdivididos que geram um erro, se encontrado. Um banco de dados subdividido é aquele em que um subconjunto de arquivos é selecionado pela lista de volumes.  Não há suporte para roll forward (restaurações diferenciais ou de log) após uma restauração por meio do Gravador do SQL.

#### <a name="restore"></a>Restaurar

O solicitante restaura os bancos de dados que foram copiados em backup no modo não baseado em componentes.  Essas restaurações não podem ser seguidas de uma restauração de roll forward, como uma restauração de log ou uma restauração diferencial.

Para operações de restauração não baseadas em componentes, a restauração precisará ser executada com a instância offline do SQL Server ou os bancos de dados de destino serão removidos/desanexados para garantir que os arquivos estejam offline.  Os arquivos são copiados no local e, em seguida, os bancos de dados anexados. Tudo isso acontece fora do escopo do Gravador do SQL.

### <a name="component-based-backup-and-restore"></a>Backup e restauração baseados em componentes

Em um backup baseado em componentes, o solicitante seleciona explicitamente os componentes do banco de dados (dos metadados que o Gravador do SQL retorna ao cliente) para backup/restauração.

#### <a name="backup"></a>Backup

Em um backup baseado em componentes, todos os volumes de backup para os bancos de dados selecionados devem ser incluídos no conjunto de instantâneos de volume.  Caso contrário, o Gravador do SQL detectará bancos de dados subdivididos (com volumes de backup fora do conjunto de instantâneos) e falhará o backup.  Um backup completo faz backup de dados do banco de dados e de todos os arquivos de log necessários para colocar o banco de dados em um estado transacionalmente consistente no momento da restauração.

#### <a name="full-restore-without-rollforward"></a>Restauração completa sem roll forward

Às vezes, uma restauração completa do backup de banco de dados é realizada sem nenhum roll forward adicional. Isso pode ser devido ao fato de que não há metadados para facilitar o roll forward ou, em alguns casos, os roll forwards não são necessários. Esta seção aborda essas duas situações brevemente.  

#### <a name="no-metadatano-rollforward"></a>Sem metadados/sem roll forward

Se nenhum metadado do gravador (metadados de backup baseados em componentes) for salvo durante a operação de backup, a restauração precisará ser executada com a instância offline do SQL Server ou os bancos de dados de destino serão removidos/desanexados para garantir que os arquivos estejam offline.  Os arquivos são copiados no local e, em seguida, os bancos de dados anexados. Tudo isso acontece fora do escopo do Gravador do SQL.

#### <a name="metadata-exist-but-no-additional-rollforward-is-needed"></a>Os metadados existem, mas nenhum roll forward adicional é necessário

O solicitante restaura os bancos de dados que foram copiados em backup no modo baseado em componentes, mas nenhum roll forward é solicitado. Nesse caso, o SQL Server executará a recuperação de pane no banco de dados como parte da restauração.

**Restauração completa com roll forwards adicionais** O solicitante pode emitir uma restauração especificando a opção SetAdditionalRestores(true).  Essa opção indica que o solicitante pretende acompanhar mais restaurações de roll forward (como restauração de log, restauração diferencial etc.). Isso instrui o SQL Server a não executar a etapa de recuperação no final da operação de restauração.

Isso só será possível se os metadados do gravador tiverem sido salvos durante o backup e estiverem disponíveis para o Gravador do SQL no momento da restauração. O serviço SQL Server precisa estar em execução antes que o solicitante instrua o VSS a executar a atividade de restauração.

O Gravador do SQL espera a seguinte sequência:

1. Preparação para restaurar cada banco de dados. Essa atividade envolve o fechamento de todos os identificadores de arquivo a fim de permitir que os arquivos de banco de dados sejam copiados/montados pelo aplicativo solicitante.
1. Os arquivos são copiados/montados pelo aplicativo solicitante.
1. Finalize a restauração (com NORECOVERY).  Os bancos de dados são colocados online, mas em um estado de "restauração".

Backups convencionais do SQL, diferencial ou logs, podem então ser usados para efetuar roll forward do banco de dados por meio do VDI/T-SQL ou aplicando a restauração diferencial usando a estrutura VSS.

### <a name="full-text-support"></a>Suporte de texto completo

O Gravador do SQL relata os contêineres de catálogo de texto completo com especificações de arquivo recursivo nos componentes de banco de dados no Documento de Metadados do Gravador.  Eles são incluídos automaticamente no backup quando o componente de banco de dados é selecionado

### <a name="differential-backuprestore"></a>Backup/restauração diferenciais

Uma operação de backup diferencial faz backup apenas dos dados que foram alterados desde o backup completo de base mais recente. Um backup diferencial contém apenas as partes dos arquivos de banco de dados que foram alteradas. Para fazer esse backup, o aplicativo de backup ou o solicitante precisará obter informações sobre a localização das alterações nos arquivos de banco de dados, de modo que as seções apropriadas dos arquivos possam ser copiadas em backup. Durante uma operação de backup diferencial, o Gravador do SQL fornece essas informações no formato especificado pelas "informações de arquivo parcial do VSS". Essas informações podem ser usadas para fazer backup apenas da parte alterada dos arquivos de banco de dados.

### <a name="backup"></a>Backup

O solicitante pode emitir um backup diferencial configurando a opção DIFFERENTIAL (**VSS_BT_DIFFERENTIAL**) no Documento de Componente de Backup (**IVssBackupComponents::SetBackupState**) ao iniciar uma operação de backup com o VSS.  O Gravador do SQL transmitirá as informações de arquivo parcial (retornadas a ele pelo SQL Server) para o VSS.  O solicitante pode obter essas informações de arquivo chamando as APIs do VSS (**IVssComponent::GetPartialFile**). Essas informações de arquivo parcial permitem que o solicitante escolha apenas os intervalos de bytes alterados para backup nos arquivos de banco de dados.

Durante a fase Tarefas pré-backup, o Gravador do SQL garantirá que exista uma só base diferencial para cada banco de dados selecionado.

Durante o evento PostSnapshot, o Gravador do SQL obterá as informações de arquivo parcial do SQL Server e as adicionará ao Documento de Componente de Backup usando a chamada a **IVssComponent::AddPartialFile**.  

  > [!NOTE]
  > O Gravador do SQL dá suporte apenas a uma só linha de base diferencial para backups diferenciais. Não há suporte para várias linhas de base.

### <a name="partial-file-information-format"></a>Formato das informações de arquivo parcial

Para cada banco de dados copiado em backup durante um backup diferencial, o Gravador do SQL armazenará as informações de arquivo parcial de cada arquivo de banco de dados. Essas informações são usadas pelo solicitante ou o aplicativo de backup para copiar apenas as partes relevantes do arquivo para a mídia de backup durante o backup real dos arquivos. Para obter mais informações sobre o formato dessas informações de arquivo parcial, confira a documentação do Serviço de Cópias de Sombra de Volume.

Um solicitante pode determinar esses arquivos chamando **IVssComponent::GetPartialFileCount** e **IVssComponent::GetPartialFile**.  **IVssComponent::GetPartialFile** retornará um caminho e um nome de arquivo que aponte para o arquivo e uma cadeia de caracteres de intervalos que indica o que precisa ser copiado em backup no arquivo.

Para obter mais informações sobre a recuperação das informações de arquivo parcial, confira a [documentação do VSS](/windows/win32/vss/volume-shadow-copy-service-overview).

### <a name="back-up-files"></a>Fazer backup de arquivos

Durante essa fase, o aplicativo de backup deve examinar os metadados do gravador armazenados no Documento de Componente de Backup e fazer backup apenas das partes relevantes dos arquivos. (Para os arquivos de catálogo de texto completo, esse backup deve ser feito com base nos carimbos de data/hora do arquivo. Isso será descrito mais adiante neste documento).

Um backup diferencial sempre será relativo ao backup de base mais recente que existe para o banco de dados.  No momento da restauração, o SQL Server detectará backups diferenciais e de base incompatíveis. Portanto, é responsabilidade do aplicativo de backup ou do administrador do sistema ter certeza de que o diferencial é relativo ao backup completo esperado.  Se algum procedimento fora de banda tiver feito outro backup completo, o aplicativo de backup poderá não ser conseguir restaurar o diferencial, pois não é "proprietário" do backup de base.

Atualmente, se as informações de intervalo de bytes (informações de arquivo parcial) forem muito grandes (excedendo 64 mil bytes no tamanho do buffer), o SQL Server gerará um erro instruindo o usuário a fazer um backup completo.

### <a name="interesting-cases-during-backup"></a>Casos interessantes durante o backup

O arquivo add/drop/shrink/growth/logical-rename/physical-rename apresenta casos interessantes no backup.

**Arquivos recém-adicionados depois de a base ser obtida**

Esses arquivos são incluídos na especificação parcial, porque todos os cabeçalhos do arquivo de Banco de Dados SQL precisam estar na especificação parcial.  Além da página de cabeçalho, todas as páginas alocadas precisam ser incluídas na especificação parcial.

**Arquivos removidos depois de a base ser obtida**

Depois que a base é obtida, os arquivos de dados podem ser removidos.  Esses arquivos não são incluídos no Documento de Metadados do Gravador durante o backup diferencial.  Além disso, não haverá informações parciais associadas ao arquivo removido.

**Arquivos reduzidos depois de a base ser obtida**

As informações parciais não são coletadas dos arquivos até as reduções de arquivo serem desabilitadas no servidor.  Isso garante que nunca incluiremos informações parciais que correspondam à região reduzida de um arquivo de dados.  

**Arquivos aumentados depois de a base ser obtida**

Se o crescimento tiver ocorrido antes de as informações parciais serem coletadas, as informações parciais deverão ter incluído as páginas alocadas na região aumentada.  Se o crescimento tiver ocorrido depois de as informações parciais serem coletadas, as informações parciais não incluirão alterações na região aumentada.  Nas seções a seguir, veremos que essas alterações serão restauradas pelo roll forward de log.

**O arquivo foi renomeado logicamente depois de a base ser obtida**

Uma renomeação lógica do arquivo não afeta o backup nem a restauração, pois o nome lógico do arquivo não é referenciado em nenhum lugar no Documento de Metadados do Gravador ou no Documento de Componente de Backup.  (Confira o Documento de Metadados do Gravador: um exemplo para obter mais detalhes.)

**Arquivo fisicamente renomeado depois de a base ser obtida**

Uma renomeação de arquivo de banco de dados físico não entrará em vigor até que o banco de dados seja reiniciado.  Portanto, as informações de configuração do banco de dados ou as informações de caminho do arquivo no buffer de informações parciais ainda são baseadas nos caminhos físicos antigos, que são os únicos caminhos válidos para esses arquivos de banco de dados no instantâneo.

### <a name="restore"></a>Restaurar

Durante uma restauração diferencial, os metadados de backup que o solicitante retorna ao Gravador do SQL têm as informações de tipo de backup.  Portanto, não é necessário nenhum tratamento especial por parte do Gravador do SQL.  O SQL Server descobrirá que essa é uma restauração diferencial por si só.  O SQL Server trata essa restauração diferencial da mesma maneira que uma restauração diferencial nativa que não é executada por meio do VSS.

### <a name="prerestore-phase"></a>Fase pré-restauração

Durante essa fase, o SQL Server redimensionará todos os arquivos para o tamanho apropriado com base nos metadados do arquivo do backup diferencial.  Se o arquivo for aumentado, o SQL Server vai zerar a parte aumentada.  Se for necessário criar um arquivo (ele foi criado após a obtenção da base), o SQL Server vai zerar o novo arquivo. Ele também fecha todos os identificadores de arquivo, de modo que o aplicativo de backup possa substituir os arquivos pelos dados restaurados da mídia de backup.

### <a name="restore-files"></a>Restaurar arquivos

O cliente deve restaurar os arquivos com base na especificação de arquivo parcial.  Os dados devem ser restaurados para o mesmo deslocamento/intervalo do arquivo de banco de dados, conforme indicado na especificação de arquivo parcial armazenada nos metadados do gravador.

O arquivo de banco de dados add/drop/growth/shrink/logical-rename/physical-rename novamente apresenta casos interessantes no momento da restauração.

**Se um arquivo de banco de dados foi adicionado depois de a base completa ser obtida**

Esses arquivos precisam ter sido pré-criados pelo SQL Server durante a fase de preparação da restauração.  Eles devem ter sido estendidos para o tamanho correto e zerados.  O cliente só precisa dispor os dados de acordo com a especificação parcial (a especificação parcial inclui todas as extensões alocadas).

**Se um arquivo de banco de dados foi removido depois de a base completa ser obtida**

As informações parciais que o SQL Server forneceu não incluem nenhuma informação de acompanhamento dessas remoções de arquivos.  O SQL Server é responsável por detectar os arquivos a serem excluídos, comparando os metadados dos arquivos restaurados com os contêineres existentes e, de fato, excluindo-os.  Isso é feito antes da restauração como uma etapa de preparação.

**Se um arquivo de banco de dados aumentou desde que a base completa foi obtida**

Esses arquivos precisam ter sido estendidos para o tamanho correto pelo SQL Server durante a fase de preparação de restauração.  A região estendida precisa ter sido zerada pelo SQL Server também.  Portanto, o cliente pode dispor os dados com segurança mesmo na região aumentada, de acordo com a especificação parcial.  Se o arquivo for aumentado após a obtenção das informações parciais, as alterações na região aumentada serão restauradas com a reprodução do log copiado em backup junto com o backup diferencial.

**Se um arquivo de banco de dados foi reduzido desde que a base completa foi obtida**

O SQL Server é responsável por truncar o arquivo para o tamanho necessário, de acordo com os metadados.  Isso é feito antes da restauração como uma etapa de preparação.

**Se um arquivo de banco de dados foi logicamente renomeado desde que a base completa foi obtida**

Isso não afetará a restauração, pois o nome lógico não aparece no Documento de Metadados do Gravador nem no Documento de Componente de Backup.  A alteração do nome lógico será restaurada quando o cliente aplicar a alteração ao arquivo de banco de dados primário, que contém as informações do catálogo do sistema.

**Se um arquivo de banco de dados foi fisicamente renomeado desde que a base completa foi obtida.**

Se, no momento do backup diferencial, a renomeação não tiver sido efetivada, o cliente ainda restaurará os dados na localização antiga.  Uma reinicialização de banco de dados após a restauração fará com que a renomeação física entre em vigor.  Se, no momento do backup diferencial, a renomeação do arquivo físico já tiver sido efetivada, os dados parciais, se houver, serão copiados em backup do novo caminho físico.  

### <a name="post-restore"></a>Pós-restauração

Durante os eventos de pós-restauração, o Gravador do SQL executará a operação normal refazer e a recuperação, se SetAdditionalRestores() for definido como False, do banco de dados.

## <a name="differential-backuprestore-for-full-text-catalogs"></a>Backup/restauração diferenciais para catálogos de texto completo

Os catálogos de texto completo do SQL Server fazem parte dos recursos de banco de dados que precisam ser copiados em backup ou restaurados junto com o restante dos arquivos de banco de dados.  Um backup diferencial é baseado no carimbo de data/hora para o catálogo de texto completo.  O backup/a restauração diferenciais do VSS SQL Server tem um só backup de base.  Em outras palavras, não haverá bases diferentes para contêineres diferentes.  Para o backup do catálogo de texto completo do VSS, isso significa que, para todos os contêineres de catálogo de texto completo, o backup diferencial será baseado em um só carimbo de data/hora, ao contrário do caso do backup diferencial do SQL nativo, no qual há uma base de carimbo de data/hora por contêiner do catálogo de texto completo.

No VSS, esse carimbo de data/hora é expresso como uma propriedade de todo o componente que é definida durante o backup completo e usada durante um próximo backup diferencial.  

### <a name="onidentify"></a>OnIdentify

Em OnIdentify, o Gravador do SQL chama IVssCreateWriterMetadata::SetBackupSchema() para definir o valor VSS_BS_TIMESTAMPED.  Isso indica para o aplicativo de backup que o Gravador do SQL é o proprietário do gerenciamento da base diferencial.

### <a name="setting-the-base-timestamp"></a>Como configurar o carimbo de data/hora base

O carimbo de data/hora base é definido durante um backup completo.  Em **OnPostSnapshot()** , o gravador invoca **IVssComponent::SetBackupStamp()** para armazenar o carimbo de data/hora com o componente no documento de backup.

### <a name="differential-backup"></a>Backup diferencial

O aplicativo de backup vai recuperar esse carimbo de data/hora do backup completo de base e disponibilizará o carimbo de data/hora ao gravador chamando **IVssComponent::GetBackupStamp()** para recuperar o carimbo base do backup de base anterior.  Em seguida, ele o disponibilizará ao gravador chamando **IVssBackupComponent::SetPreviousBackupStamp()** .  Em seguida, o gravador recupera o carimbo chamando **IVssComponent::GetPreviousBackupStamp()** e o converte em um carimbo de data/hora usado para **IVssComponent::AddDifferencedFilesByLastModifyTime()** .  

**Responsabilidade do aplicativo de backup durante um backup diferencial** Durante um backup diferencial, o aplicativo de backup é responsável por:

- Fazer backup de qualquer arquivo (todo o arquivo) cujo carimbo de data/hora modificado pela última vez é maior que o carimbo de data/hora especificado pela "hora da última modificação" para o conjunto de arquivos no componente.
- Acompanhar e detectar os arquivos excluídos.  

**Responsabilidades do aplicativo de backup durante uma restauração diferencial** Durante uma restauração diferencial, o aplicativo de backup é responsável por:

- Restaurar todos os arquivos dos quais foi feito backup, criando um arquivo (caso ele ainda não exista) ou substituindo um arquivo existente (caso ele já exista).
- Aumentar o arquivo antes de dispor o conteúdo se o arquivo restaurado for maior que o arquivo existente.
- Truncar o arquivo para o mesmo tamanho do arquivo restaurado se o arquivo restaurado é menor que o arquivo existente.
- Excluir todos os arquivos que devem ser excluídos; ou seja, os arquivos que não devem existir começando no ponto no tempo do backup diferencial.

### <a name="copy-only-backup"></a>Backup somente cópia

Às vezes, é necessário fazer um backup destinado a uma finalidade especial. Por exemplo, talvez seja necessário fazer uma cópia de um banco de dados para fins de teste.  Esse backup não deve afetar os procedimentos gerais de backup e restauração do banco de dados. O uso da opção COPY_ONLY especifica que o backup é feito "fora de banda" e não deve afetar a sequência normal de backups. O Gravador do SQL dá suporte ao tipo de backup "somente cópia" com instâncias do SQL Server.

Durante a fase de descoberta de backup, o Gravador do SQL indicará a capacidade de fazer um backup somente cópia configurando a opção de esquema de backup compatível VSS_BS_COPY usando a chamada **IVssCreateWriterMetadata::SetBackupSchema**. O solicitante pode definir o tipo de backup como um backup somente cópia configurando a opção VSS_BACKUP_TYPE como VSS_BT_COPY com a chamada **IVssBackupComponents::SetBackupState**.

Quando um backup somente cópia é selecionado, pressupõe-se que os arquivos em disco serão copiados para uma mídia de backup (pelo solicitante), seja qual for o estado do histórico de backup de cada arquivo. O SQL Server não atualizará o histórico de backup. Esse tipo de backup não constituirá como um backup de base para operações adicionais de backup diferencial e também não perturbará o histórico dos backups diferenciais anteriores.

### <a name="restore-with-move"></a>Restauração com movimentação

O VSS permite que o aplicativo de backup (solicitante) especifique um novo destino de restauração usando a chamada **IVssComponent::SetNewTarget**.  Em PreRestore() e PostRestore(), o Gravador do SQL verifica se há, pelo menos, um novo destino especificado. É responsabilidade do aplicativo de backup copiar fisicamente os arquivos para a nova localização no momento da restauração/da cópia real do arquivo.

O aplicativo de backup só tem permissão para especificar novos destinos para o caminho físico, mas não para a especificação de arquivo.  Por exemplo, para um arquivo de banco de dados localizado em c:\data\test.mdf, o nome de arquivo real, test.mdf, não pode ser alterado.  Somente o caminho c:\data pode ser alterado.  Para um contêiner do catálogo de texto completo localizado em c:\ftdata\foo, como a especificação de arquivo no VSS é "*" e a especificação de caminho no VSS é c:\ftdata\foo, o caminho inteiro pode ser alterado.  

### <a name="database-rename"></a>Renomeação de banco de dados

Um solicitante poderá precisar restaurar um Banco de Dados SQL com um novo nome, especialmente se o banco de dados for restaurado lado a lado com o banco de dados original.  Essa opção pode ser especificada pelo solicitante durante a operação de restauração configurando uma opção de restauração personalizada como "Nome do Novo Componente" = <"Novo Nome"> usando a chamada do VSS **IVssBackupComponents::SetRestoreOptions()** (no parâmetro wszRestoreOptions).

O Gravador do SQL usará todo o conteúdo do valor do Novo Nome do Componente e o usará como o novo nome do banco de dados restaurado. Se nenhuma opção for especificada, o SQL restaurará o banco de dados com o nome original (nome do componente).

  > [!NOTE]
  > Atualmente, o Gravador do SQL não dá suporte à "renomeação entre instâncias" para mover um banco de dados para uma nova instância.

### <a name="auto-recovered-snapshots"></a>Instantâneos recuperados automaticamente

Normalmente, um instantâneo de um banco de dados do SQL Server obtido com a estrutura VSS está em um estado não recuperado. Os dados no instantâneo não podem ser acessados com segurança antes de passarem pela fase de recuperação para reverter as transações em andamento e colocar o banco de dados em um estado consistente. Como o instantâneo está em um estado somente leitura, ele não pode ser recuperado pelo processo normal de anexação do banco de dados.

É possível recuperar automaticamente os instantâneos como parte do processo de criação de instantâneo. Como parte do documento de metadados do gravador, o Gravador do SQL especificará o sinalizador de componente "VSS_CF_APP_ROLLBACK_RECOVERY" para indicar que a recuperação precisa ser executada para o banco de dados no instantâneo antes que o banco de dados possa ser acessado ao especificar o conjunto de instantâneos, o solicitante pode indicar que o instantâneo deve ser um instantâneo de reversão de aplicativo (ou seja, todos os arquivos de banco de dados em um instantâneo devem estar em um estado consistente para uso do aplicativo) ou um instantâneo de backup (um instantâneo usado para fazer backup dos dados a serem restaurados mais tarde, em caso de falha do sistema).

O solicitante deve definir VSS_VOLSNAP_ATTR_ROLLBACK_RECOVERY para indicar que o backup desse componente está sendo feito para uma finalidade que não seja de backup.  Em seguida, o VSS correlacionará VSS_CF_APP_ROLLBACK_RECOVERY especificado pelo Gravador do SQL no componente selecionado com VSS_VOLSNAP_ATTR_ROLLBACK_RECOVERY e determinará se a recuperação automática está ocorrendo.  O VSS tornará o instantâneo gravável por um período limitado e adicionará automaticamente o bit de VSS_VOLSNAP_ATTR_AUTORECOVERY ao contexto do instantâneo.

No caso do SQL Server, a recuperação automática deve ser aplicada somente aos instantâneos de reversão de aplicativo, mas não aos instantâneos de backup. Para instantâneos de reversão de aplicativo, um processo de recuperação automática é iniciado pelo Gravador do SQL durante o evento PostSnapShot. Esse processo fará o seguinte para cada banco de dados do SQL Server explicitamente selecionado (pelo solicitante) no conjunto de instantâneos:

- Anexar o banco de dados de instantâneo à instância original do SQL Server (ou seja, a instância à qual o banco de dados original está anexado).
- Recuperar o banco de dados (isso ocorre como parte da operação de "anexação").
- Reduzir os arquivos de log.

    Isso reduz a quantidade de "cópia na gravação" desnecessária que precisa ser feita pela estrutura VSS, caso o provedor VSS seja um "provedor de software". A redução dos arquivos de log é o comportamento padrão. Isso pode ser desabilitado pela configuração do valor da chave do Registro a seguir como 1.
    
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SQLWriter\
    Settings\DisableLogShrink
    
    Isso pode ser útil em cenários nos quais o instantâneo possa ser usado para exportar dados de uma página específica (em um ponto específico no tempo) do log para corrigir um problema no banco de dados online.

- Desanexe o banco de dados.

Agora temos um instantâneo consistente e recuperado que pode ser anexado para consulta.

### <a name="multi-database-transactions"></a>Transações de vários bancos de dados

Em alguns casos, os bancos de dados de instantâneos podem conter algumas transações de vários bancos de dados em andamento. Durante a operação de recuperação, o Gravador do SQL anexará o banco de dados nos instantâneos com a opção Anulação Presumida. Isso reverterá qualquer transação de vários bancos de dados que ainda não esteja confirmada (incluindo as transações que estão em um estado Preparado para Confirmação). Isso poderá resultar em algumas inconsistências entre bancos de dados no conjunto de instantâneos. Por exemplo, considere dois bancos de dados, A e B. Há uma transação distribuída entre esses dois bancos de dados e essa transação está no estado Confirmado no banco de dados A e no estado Preparado para Confirmação no banco de dados B. Como parte do processo de recuperação automática, essa transação será confirmada no banco de dados A e revertida no banco de dados B. Isso poderá resultar em algumas inconsistências no conjunto de instantâneos.

O componente MS DTC (Coordenador de Transações Distribuídas da Microsoft) a ser lançado no período do Longhorn pela estrutura VSS corrigirá esse problema de inconsistência em transações que abrangem bancos de dados em instâncias do SQL Server. A próxima versão do SQL Server corrigirá essas inconsistências em transações que abrangem bancos de dados em uma instância do SQL Server.

### <a name="security-implications-for-autorecovered-snapshots"></a>Implicações de segurança para instantâneos recuperados automaticamente

Para os instantâneos do VSS, após a recuperação automática, os arquivos serão protegidos com ACLs (listas de controle de acesso) para permitir o acesso somente ao grupo interno especial ao qual a conta do SQL Server pertence.  Isso significa que um membro do administrador de caixa ou desse grupo especial poderá anexar o banco de dados. O cliente que solicita uma anexação dos arquivos de banco de dados em um instantâneo deve ser membro de Builtin/Administrators ou da conta do SQL Server.

### <a name="special-cases"></a>Casos especiais

Esta seção descreve alguns dos casos especiais encontrados durante as operações de backup e restauração baseadas no Gravador do SQL.

#### <a name="autoclose-databases"></a>Bancos de dados de fechamento automático

Para backups não baseados em componentes, o fechamento automático de bancos de dados é feito ao verificar se há condições subdivididas, mas os bancos de dados fechados automaticamente não são explicitamente congelados durante as operações de backup.

O cenário esperado aqui é que muitos bancos de dados fechados possam existir e queremos minimizar o custo do instantâneo.  Em geral, os bancos de dados fechados automaticamente são usados em configurações de baixo nível na qual os recursos são escassos.

#### <a name="file-list"></a>Lista de arquivos

A lista de arquivos para cada banco de dados é determinada durante uma etapa de enumeração antes do evento Preparação do Backup.  Se a lista de arquivos de banco de dados for alterada entre a enumeração e o congelamento, o banco de dados poderá ser subdividido, a menos que o aplicativo verifique novamente a lista de arquivos. Não esperamos que isso seja um problema, mas é algo de que os fornecedores precisam estar cientes.

#### <a name="stopped-instances"></a>Instâncias interrompidas

Se uma instância do SQL Server não estiver em execução no momento em que a etapa de enumeração ocorrer, nenhum dos bancos de dados dessas instâncias poderá ser selecionado.

Se uma instância for interrompida no intervalo entre a enumeração e o evento Preparação do Backup, todos os bancos de dados na instância interrompida serão ignorados.

#### <a name="system-and-user-databases"></a>Bancos de dados de sistema e de usuário

Os bancos de dados de sistema no SQL Server incluem os bancos de dados mestre, modelo e msdb que são enviados e instalados como parte do SQL Server. Esta seção descreve como esses bancos de dados são tratados em um processo de backup de instantâneo do VSS.

### <a name="system-databases"></a>Bancos de dados do sistema

O banco de dados mestre só pode ser restaurado com a interrupção da instância, a substituição dos arquivos de banco de dados (feita pelo aplicativo de backup) e, em seguida, a reinicialização da instância. Não é possível efetuar roll forward.

O Gravador do SQL dá suporte à restauração dos bancos de dados modelo e msdb online, sem desligar a instância.


#### <a name="simple-recovery-model-user-databases"></a>Bancos de dados de usuário do modelo de recuperação simples

Se o banco de dados mestre for restaurado junto com os bancos de dados de usuário que estão usando o modelo de recuperação simples, os bancos de dados de usuário poderão ser restaurados com a mesma técnica do banco de dados mestre: com a instância desligada, apenas copie ou monte os volumes.  Quando a instância do SQL for iniciada, tudo será recuperado.

#### <a name="rolling-forward-user-databases"></a>Como efetuar roll forward de bancos de dados de usuário

Se os bancos de dados de usuário forem recuperados e submetidos a roll forward junto com a recuperação do banco de dados mestre, a instância não deverá iniciar e recuperar os bancos de dados mestre e de usuário juntos.

O procedimento é o seguinte:

1. Verifique se a instância do SQL Server foi interrompida.
1. Execute a restauração em duas fases.
    1. Restaure os bancos de dados de sistema e os bancos de dados de usuário que devem ser recuperados ao mesmo tempo (ou seja, os bancos de dados de usuário do modo de recuperação simples) por meio da cópia de arquivo/da montagem de volume com o VSS.
        1. Se os bancos de dados de usuário para roll forward não estiverem no mesmo volume dos bancos de dados de sistema, esse volume não deverá ser retornado no momento. Este cenário exige planejamento antes do backup.
        1. Se os bancos de dados de usuário estiverem no mesmo volume dos bancos de dados de sistema, os bancos de dados de usuário precisarão ser ocultados do SQL Server.
    1. Inicie a instância do SQL Server usando o parâmetro -f.  (Ao usar a opção de inicialização -f, somente o banco de dados mestre pode ser restaurado.)
        1. Emita um ALTER DATABASE \<x> SET OFFLINE para cada banco de dados a ser submetido a roll forward.  (A desanexação do banco de dados é uma alternativa)
        1. Interrompa a instância do SQL Server.
        1. Inicie a instância do SQL Server (os arquivos dos bancos de dados de usuário a serem submetidos a roll forward não são visíveis para o SQL Server).

Use o VSS para restaurar os bancos de dados de usuário usando WITH NORECOVERY, conforme descrito em "Restauração completa com roll forward".

## <a name="appendix"></a>Apêndice

### <a name="writer-metadata-document--an-example"></a>Documento de Metadados do Gravador:  um exemplo

Considerando um banco de dados de exemplo chamado DB1, que pertença à instância Instance1 do SQL Server no computador Server1 e que contenha os seguintes arquivos de banco de dados/log:

- Arquivo de banco de dados chamado "primary" armazenado em c:\db\DB1.mdf
- Arquivo de banco de dados chamado "secondary" armazenado em c:\db\DB1.ndf
- Arquivo de log do banco de dados chamado "log" armazenado em c:\db\DB1.ldf
- Catálogo de texto completo chamado "foo" armazenado no diretório c:\db\ftdata\foo
- Catálogo de texto completo chamado "bar" armazenado no diretório c:\db\ftdata\bar.

Estes são os metadados do gravador do banco de dados:

**Componente de grupo de arquivos no nível de banco de dados**

- ComponentType: VSS_CT_FILEGROUP
- LogicalPath: "Server1\Instance1"
- ComponentName: "DB1"
- Caption: NULO
- pbIcon: NULO
- cbIcon: 0
- bRestoreMetadata: FALSE
- NotifyOnBackupComplete: TRUE
- Selectable: TRUE
- SelectableForRestore: TRUE
- ComponentFlags: VSS_CF_APP_ROLLBACK_RECOVERY

**Arquivo de grupo de arquivos**

- LogicalPath: "Server1\Instance1"
- GroupName: "DB1"
- Path: "c:\db"
- FileSpec: "DB1.mdf"
- Recursive: FALSE
- AlternatePath: NULO
- BackupTypeMask: VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED
- Arquivo de grupo de arquivos
- LogicalPath: "Server1\Instance1"
- GroupName: "DB1"
- Path: "c:\db"
- FileSpec: "DB1.ndf"
- Recursive: FALSE
- AlternatePath: NULO
- BackupTypeMask: VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**Arquivo de grupo de arquivos**

- LogicalPath: "Server1\Instance1"
- GroupName: "DB1"
- Path: "c:\db"
- FileSpec: "DB1.ldf"
- Recursive: FALSE
- AlternatePath: NULO
- BackupTypeMask: VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**Arquivo de grupo de arquivos:**

- LogicalPath: "Server1\Instance1"
- GroupName: "DB1"
- Path: "c:\db\ftdata\foo"
- FileSpec: "*"
- Recursive: TRUE
- AlternatePath: NULO
- BackupTypeMask: VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

**Arquivo de grupo de arquivos:**

- LogicalPath: "Server1\Instance1"
- GroupName: "DB1"
- Path: "c:\db\ftdata\bar"
- FileSpec: "*"
- Recursive: TRUE
- AlternatePath: NULO
- BackupTypeMask: VSS_FSBT_ALL_BACKUP_REQUIRED | VSS_FSBT_ALL_SNAPSHOT_REQUIRED

Se a instância do servidor for a instância padrão no computador, o caminho lógico se tornará uma parte: "Server1".


    
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backups somente cópia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [Guia de arquitetura e gerenciamento de log de transações do SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
