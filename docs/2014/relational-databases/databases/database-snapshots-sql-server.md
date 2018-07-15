---
title: Instantâneos do banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- static database views
- snapshots [SQL Server database snapshots]
- source databases [SQL Server]
- snapshots [SQL Server database snapshots], about database snapshots
- database snapshots [SQL Server]
- read-only database views
- database snapshots [SQL Server], about database snapshots
ms.assetid: 00179314-f23e-47cb-a35c-da6f180f86d3
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c478f8a5d60d2604b95146fc1a712742e3f3420
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320396"
---
# <a name="database-snapshots-sql-server"></a>Instantâneos de banco de dados (SQL Server)
  Um instantâneo de banco de dados é uma exibição estática somente leitura de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (o *banco de dados de origem*). O instantâneo de banco de dados é transacionalmente consistente com o banco de dados de origem a partir do momento da criação do instantâneo. Um instantâneo de um banco de dados sempre reside na mesma instância de servidor que o banco de dados de origem. Quando o banco de dados de origem é atualizado, o instantâneo do banco de dados é atualizado. Portanto, quanto mais tempo o instantâneo de banco de dados existir, maior será a probabilidade de ele usar todo o espaço em disco disponível.  
  
 Vários instantâneos podem existir em um banco de dados de origem. Cada instantâneo de banco de dados persiste até que seja explicitamente removido pelo proprietário do banco de dados.  
  
> [!NOTE]  
>  Os instantâneos de banco de dados não estão relacionados a backups de instantâneos, isolamento de instantâneo de transações ou replicação de instantâneo.  
  
 **Neste tópico:**  
  
-   [Visão geral do recurso](#FeatureOverview)  
  
-   [Benefícios dos instantâneos de banco de dados](#Benefits)  
  
-   [Termos e definições](#TermsAndDefinitions)  
  
-   [Pré-requisitos e limitações dos instantâneos de banco de dados](#LimitationsRequirements)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="FeatureOverview"></a> Visão geral do recurso  
 Os instantâneos do banco de dados funcionam no nível da página de dados. Antes que uma página do banco de dados de origem seja modificada pela primeira vez, a página original é copiada do banco de dados de origem ao instantâneo. O instantâneo armazena a página original, preservando os registros de dados da forma como existiam quando o instantâneo foi criado. O mesmo processo é repetido para todas as páginas modificadas pela primeira vez. Para o usuário, um instantâneo do banco de dados parece nunca ser alterado, porque as operações de leitura em um instantâneo do banco de dados sempre acessam as páginas de dados originais, independentemente de onde elas residam.  
  
 Para armazenar as páginas originais copiadas, o instantâneo usa um ou mais *arquivos esparsos*. Inicialmente, um arquivo esparso é, essencialmente, um arquivo vazio que não contém dados de usuário e no qual ainda não foi alocado espaço em disco para os dados do usuário. À medida que mais páginas são atualizadas no banco de dados de origem, o tamanho do arquivo aumenta. A figura a seguir mostra os efeitos de dois padrões de atualização contrastantes no tamanho de um instantâneo. O padrão de atualização A reflete um ambiente em que apenas 30% das páginas originais são atualizadas durante a vida do instantâneo. O padrão de atualização B reflete um ambiente em que 80% das páginas originais são atualizadas durante a vida do instantâneo.  
  
 ![Padrões de atualização alternativos e tamanho do instantâneo](../../database-engine/media/dbview-04.gif "Padrões de atualização alternativos e tamanho do instantâneo")  
  
##  <a name="Benefits"></a> Benefícios dos instantâneos de banco de dados  
  
-   Os instantâneos podem ser utilizados para fins de geração de relatórios.  
  
     Os clientes podem consultar um instantâneo do banco de dados, o que é útil para gravar relatórios com base nos dados no momento da criação do instantâneo.  
  
-   Manutenção de dados históricos para geração de relatórios.  
  
     Um instantâneo pode estender o acesso a dados do usuário em um momento determinado. Por exemplo, você pode criar um instantâneo do banco de dados ao término de um determinado período (como um trimestre financeiro) para geração posterior de relatório. Você pode executar relatórios de fim de período no instantâneo. Se o espaço em disco permitir, você também poderá manter os instantâneos de fim de período indefinidamente, permitindo consultas aos resultados desses períodos; por exemplo, para investigar o desempenho organizacional.  
  
-   Usando um banco de dados espelho mantido para fins de disponibilidade para descarregar relatórios.  
  
     O uso de instantâneos com espelhamento de banco de dados permite tornar os dados no servidor espelho acessíveis para geração de relatórios. Além disso, a execução de consultas no banco de dados espelho pode liberar recursos no banco de dados principal. Para obter mais informações, consulte [Espelhamento de banco de dados e instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md).  
  
-   Protegendo dados de erros administrativos.  
  
-   No caso de um erro do usuário em um banco de dados de origem, você poderá reverter o banco de dados de origem ao estado em que estava quando um instantâneo de banco de dados foi criado. A perda de dados é limitada às atualizações no banco de dados desde a criação do instantâneo.  
  
     Por exemplo, antes de fazer atualizações maiores, como uma atualização em massa ou uma alteração de esquema, a criação de um instantâneo do banco de dados protegerá os dados. Se cometer um erro, você poderá usar o instantâneo para recuperar o banco de dados ao revertê-lo para o instantâneo. A reversão é potencialmente muito mais rápida para essa finalidade do que a restauração a partir de um backup; porém, você não poderá efetuar roll forward posteriormente.  
  
    > [!IMPORTANT]  
    >  A reversão não funciona em um banco de dados offline ou corrompido. Portanto, é necessário fazer backups e testar regularmente seu plano de restauração para proteger um banco de dados.  
  
    > [!NOTE]  
    >  Os instantâneos do banco de dados são dependentes do banco de dados de origem. Portanto, o uso de instantâneos do banco de dados para reverter um banco de dados não é um substituto da estratégia de backup e restauração. A execução de todos os backups agendados continua essencial. Se for necessário restaurar o banco de dados de origem para o momento determinado em que o instantâneo foi criado, implemente uma política de backup que permita fazer isso.  
  
-   Protegendo dados de erros do usuário.  
  
     Com a criação regular de instantâneos do banco de dados, você pode reduzir o impacto de um erro maior do usuário, como uma tabela descartada. Para um alto nível de proteção, você pode criar uma série de instantâneos do banco de dados que abrangem tempo suficiente para reconhecer e responder à maioria dos erros de usuário. Por exemplo, de acordo com os recursos de seu disco, você pode manter de 6 a 12 instantâneos móveis abrangendo um intervalo de 24 horas. Portanto, sempre que um novo instantâneo é criado, o mais antigo pode ser excluído.  
  
    -   Para se recuperar de um erro de usuário, você pode reverter imediatamente o banco de dados ao instantâneo antes do erro. A reversão é potencialmente muito mais rápida para essa finalidade do que a restauração a partir de um backup; porém, você não poderá efetuar roll forward posteriormente.  
  
    -   Alternativamente, você pode reconstruir manualmente uma tabela descartada ou outros dados perdidos a partir das informações em um instantâneo. Por exemplo, você pode copiar os dados em massa fora do instantâneo no banco de dados e mesclar manualmente os dados de volta ao banco de dados.  
  
    > [!NOTE]  
    >  Seus motivos para usar instantâneos do banco de dados determinam quantos instantâneos simultâneos são necessários em um banco de dados, com que frequência um instantâneo deve ser criado e por quanto tempo deve ser mantido.  
  
-   Gerenciando um banco de dados de teste  
  
     Em um ambiente de teste, pode ser útil manter dados idênticos no início de cada sessão de testes ao executar um protocolo de teste repetidamente para o banco de dados. Antes de executar a primeira sessão, um testador ou desenvolvedor de aplicativos pode criar um instantâneo do banco de dados no banco de dados de teste. Depois de cada execução do teste, o banco de dados poderá retornar rapidamente ao seu estado anterior por meio da reversão do instantâneo do banco de dados.  
  
##  <a name="TermsAndDefinitions"></a> Termos e definições  
 instantâneo do banco de dados  
 Uma exibição estática somente leitura transacionalmente consistente de um banco de dados (o banco de dados de origem).  
  
 banco de dados de origem  
 No caso de um instantâneo de banco de dados, é o banco de dados no qual o instantâneo foi criado. Os instantâneos do banco de dados são dependentes do banco de dados de origem. Os instantâneos de um banco de dados devem estar na mesma instância de servidor que o banco de dados. Além disso, se o banco de dados ficar indisponível por qualquer razão, todos os seus instantâneos do banco de dados também ficarão indisponíveis.  
  
 arquivo esparso  
 Um arquivo fornecido pelo sistema de arquivos NTFS que requer muito menos espaço em disco do que seria necessário de outra forma. Um arquivo esparso é usado para armazenar páginas copiadas para um instantâneo de banco de dados. Quando criado, um arquivo esparso ocupa pouco espaço em disco. Conforme os dados são gravados em um instantâneo de banco de dados, o NTFS aloca gradualmente espaço em disco no arquivo esparso correspondente.  
  
##  <a name="LimitationsRequirements"></a> Pré-requisitos e limitações dos instantâneos de banco de dados  
 **Nesta seção:**  
  
-   [Pré-requisitos](#Prerequisites)  
  
-   [Limitações do banco de dados de origem](#LimitsOnSourceDb)  
  
-   [Limitações em instantâneos do banco de dados](#LimitsOnDbSS)  
  
-   [Requisitos de espaço em disco](#DiskSpace)  
  
-   [Instantâneos do banco de dados com grupos de arquivos offline](#OfflineFGs)  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 O banco de dados de origem, que pode usar qualquer modelo de recuperação, deve atender aos seguintes pré-requisitos:  
  
-   A instância de servidor deve estar sendo executada em uma edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que oferece suporte a instantâneos de banco de dados. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   O banco de dados de origem precisa estar online, a menos que se trate de um banco de dados espelho dentro de uma sessão de espelhamento de banco de dados.  
  
-   Você pode criar um instantâneo de banco de dados em qualquer banco de dados primário ou secundário em um grupo de disponibilidade. A função de réplica deve ser PRIMARY ou SECONDARY, em vez de estar no estado RESOLVING.  
  
     É recomendável que o estado de sincronização de banco de dados seja SYNCHRONIZING ou SYNCHRONIZED quando você criar um instantâneo de banco de dados. No entanto, os instantâneos de banco de dados poderão ser criados quando o estado de sincronização de banco de dados for NOT SYNCHRONIZING.  
  
     Para obter mais informações, confira [Instantâneos do banco de dados com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md).  
  
-   Para criar um instantâneo do banco de dados em um banco de dados espelho, o banco de dados precisa estar no estado de espelhamento SYNCHRONIZED.  
  
-   O banco de dados de origem não pode ser configurado como banco de dados compartilhado escalonável.  
  
> [!NOTE]  
>  Todo modelo de recuperação oferece suporte a instantâneos do banco de dados.  
  
###  <a name="LimitsOnSourceDb"></a> Limitações do banco de dados de origem  
 Se houver um instantâneo do banco de dados, as seguintes limitações existirão no banco de dados de origem do instantâneo:  
  
-   O banco de dados não pode ser eliminado, desanexado nem restaurado.  
  
    > [!NOTE]  
    >  O backup do banco de dados de origem funciona normalmente e não é afetado pelos instantâneos do banco de dados.  
  
-   O desempenho é reduzido, em razão do aumento de E/S no banco de dados de origem, resultante de uma operação COW (copy-on-write), para o instantâneo, toda vez que uma página é atualizada.  
  
-   Os arquivos não podem ser eliminados do banco de dados de origem nem de nenhum instantâneo.  
  
###  <a name="LimitsOnDbSS"></a> Limitações em instantâneos do banco de dados  
 As limitações a seguir aplicam-se a instantâneos do banco de dados:  
  
-   É preciso criar um instantâneo do banco de dados, a ser mantido na mesma instância de servidor, como banco de dados de origem.  
  
-   Instantâneos do banco de dados sempre funcionam em todo o banco de dados.  
  
-   Os instantâneos de banco de dados são dependentes do banco de dados de origem e não são um armazenamento redundante. Eles não oferecem proteção contra erros de disco ou outros tipos de danos. Portanto, o uso de instantâneos do banco de dados para reverter um banco de dados não é um substituto da estratégia de backup e restauração. A execução de todos os backups agendados continua essencial. Se for necessário restaurar o banco de dados de origem para o momento determinado em que o instantâneo foi criado, implemente uma política de backup que permita fazer isso.  
  
-   Quando uma página que está sendo atualizada no banco de dados de origem é impulsionada para um instantâneo, caso o instantâneo fique sem espaço em disco suficiente ou encontre outro erro, ele se tornará suspeito e deverá ser excluído.  
  
-   Os instantâneos são somente leitura. Como elas são somente de leitura, não podem ser atualizados. Portanto, não se espera que os instantâneos de banco de dados sejam viáveis após uma atualização.  
  
-   Instantâneos dos bancos de dados **modelo**, **mestre**e **tempdb** são proibidos.  
  
-   Você não pode alterar nenhuma das especificações dos arquivos de instantâneos do banco de dados.  
  
-   Você não pode cancelar arquivos de um instantâneo do banco de dados.  
  
-   Você não pode fazer backup nem restaurar instantâneos do banco de dados.  
  
-   Você não pode anexar nem desanexar instantâneos do banco de dados.  
  
-   Você não pode criar instantâneos do banco de dados em sistema de arquivos FAT32 nem em partições RAW. Os arquivos esparsos usados por instantâneos do banco de dados são fornecidos pelo sistema de arquivos NTFS.  
  
-   A indexação de texto completo não tem suporte em instantâneos do banco de dados. Os catálogos de texto completo não são propagados do banco de dados de origem.  
  
-   Um instantâneo do banco de dados herda as restrições de segurança de seu banco de dados de origem no momento da criação do instantâneo. Como os instantâneos são somente leitura, as permissões herdadas não podem ser alteradas e as alterações feitas à origem não serão refletidas nos instantâneos existentes.  
  
-   Um instantâneo sempre reflete o estado dos grupos de arquivos no momento de sua criação: grupos de arquivos online permanecem online e grupos de arquivos offline permanecem offline. Para obter mais informações, consulte "Instantâneos do banco de dados com grupos de arquivos offline", posteriormente neste tópico.  
  
-   Se um banco de dados de origem se tornar RECOVERY_PENDING, seus instantâneos do banco de dados podem se tornar inacessíveis. Depois que o problema do banco de dados de origem for resolvido, porém, seus instantâneos deverão se tornar novamente disponíveis.  
  
-   A reversão não tem suporte para grupos de arquivos somente leitura e para grupos de arquivos compactados. As tentativas de reverter um banco de dados que contenha qualquer um desses tipos de grupos de arquivos falharão.  
  
-   Em uma configuração de envio de logs, poderão ser criados instantâneos do banco de dados apenas no banco de dados primário, não em um banco de dados secundário. Se as funções entre a instância do servidor primário e a instância do servidor secundário forem alternadas, será necessário cancelar todos os instantâneos antes de definir o banco de dados primário como o banco de dados secundário.  
  
-   Um instantâneo do banco de dados não pode ser configurado como um banco de dados compartilhado escalonável.  
  
-   Os grupos de arquivos FILESTREAM não são suportados pelos instantâneos do banco de dados. Se houver grupos de arquivos FILESTREAM em um banco de dados de origem, eles serão marcados como offline nos instantâneos do banco de dados, e os instantâneos não poderão ser usados para reverter o banco de dados.  
  
    > [!NOTE]  
    >  Uma instrução SELECT executada em um instantâneo de banco de dados não deve especificar uma coluna FILESTREAM. Caso contrário, a mensagem de erro a seguir será retornada: `Could not continue scan with NOLOCK due to data movement.`  
  
-   Quando estatísticas em um instantâneo somente leitura estão ausentes ou ficam obsoletas, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria e mantém estatísticas temporárias em tempdb. Para obter mais informações, consulte [Statistics](../statistics/statistics.md).  
  
###  <a name="DiskSpace"></a> Requisitos de espaço em disco  
 Os instantâneos do banco de dados consomem espaço em disco. Se um instantâneo do banco de dados for executado sem espaço em disco suficiente, ficará marcado como suspeito e precisará ser cancelado. (O banco de dados de origem, porém, não é afetado; as suas ações prosseguem normalmente.) Em comparação com uma cópia completa de banco de dados, no entanto, os instantâneos são altamente eficazes em termos de espaço. Um instantâneo requer apenas armazenamento suficiente para as páginas alteradas no decorrer de seu tempo de vida. Em geral, os instantâneos são mantidos por certo período, de modo que o tamanho deles não é a principal preocupação.  
  
 Quanto mais tempo o instantâneo for mantido, mais provável se torna que ele venha a gastar espaço disponível. O tamanho máximo de crescimento de um arquivo esparso é o tamanho do arquivo de banco de dados de origem correspondente, no momento da criação do instantâneo.  
  
 Se um instantâneo do banco de dados for executado sem espaço em disco suficiente, precisará ser excluído (cancelado).  
  
> [!NOTE]  
>  Com exceção do espaço em arquivo, o instantâneo do banco de dados consome basicamente tanto recurso quanto o banco de dados.  
  
###  <a name="OfflineFGs"></a> Instantâneos do banco de dados com grupos de arquivos offline  
 Os grupos de arquivos offline no banco de dados de origem afetam os instantâneos do banco de dados quando se tenta realizar o seguinte:  
  
-   Criar um instantâneo  
  
     Quando um banco de dados de origem possui um ou mais grupos de arquivos offline, a criação do instantâneo terá êxito nos grupos de arquivos offline. Os arquivos esparsos não são criados para grupos de arquivos offline.  
  
-   Pegar um grupo de arquivos offline  
  
     Você pode pegar um arquivo offline no banco de dados de origem. No entanto, o grupo de arquivos permanece online nos instantâneos do banco de dados se estava online no momento da criação do instantâneo. Se os dados consultados tiverem sido alterados desde a criação do instantâneo, a página de dados original ficará acessível no instantâneo. Porém, as consultas que usam o instantâneo para acessar os dados não modificados no grupo de arquivos talvez falhem e apresentem erros de E/S (entrada/saída).  
  
-   Colocar um grupo de arquivos online  
  
     Você não pode colocar um grupo de arquivos online em um banco de dados que tenha instantâneos do banco de dados. Se um grupo de arquivos estiver offline no momento da criação do instantâneo, ou se for colocado offline quando existir um instantâneo do banco de dados, o grupo de arquivos permanecerá offline. Isto ocorre porque colocar um arquivo de novo online envolve sua restauração, o que não é possível se houver um instantâneo do banco de dados no banco de dados.  
  
-   Reverter o banco de dados de origem a um instantâneo  
  
     Reverter um banco de dados de origem em um instantâneo do banco de dados requer que todos os grupos de arquivos fiquem online, com exceção de grupos de arquivos que estavam offline quando o instantâneo foi criado.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
  
-   [Reverter um banco de dados a um instantâneo do banco de dados](revert-a-database-to-a-database-snapshot.md)  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Espelhamento de banco de dados e instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
