---
title: Introdução à nuvem híbrida do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 93282199db986ab8bcf18b05f9ae8b61a5a45b9a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926737"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introdução à nuvem híbrida do SQL Server 2014
 A maioria dos aplicativos têm alguns desafios principais, como a alta eficiência, valor comercial, configurações de hardware complexas, picos maciços sob demanda, e a conformidade com a indústria e os regulamentos corporativos. Considerando que todos esses fatores e a criação de uma tecnologia a nível empresarial possam ser muito desafiadores. A estratégia de nuvem híbrida da Microsoft oferece suporte para a nuvem tradicional, nuvem particular, nuvem pública, e os ambientes de nuvem híbridos para superar esses desafios fundamentais. 
 
 Quando sua empresa exige uma infraestrutura de ti flexível que pode ser dimensionada sob demanda, você pode criar uma nuvem privada em seu data center ou em uma nuvem pública nos data centers globais do Azure. Quando você estende o data center para localizar a nuvem pública, você cria um modelo de nuvem híbrido. 
 
 Este tópico apresenta os recursos do SQL Server 2014 que suportam cenários de nuvem híbrida. Para obter informações detalhadas sobre a estratégia de nuvem híbrida da Microsoft e o SQL Server, consulte o site [TI híbrida do SQL Server](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure e nuvem híbrida 
 Usando as tecnologias da Microsoft, você pode executar o código localmente ou na nuvem, executar na nuvem usando dados locais, ou executar totalmente na nuvem usando mais de um data center. Portanto, você pode mover seus aplicativos para a nuvem em seu próprio local enquanto preserva o valor dos investimentos de TI herdade. 
 
 Neste artigo, nos concentraremos nos cenários de nuvem híbrida que se estendem do SQL Server local para ofertas de nuvem pública do Azure: [SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj823132.aspx) e [armazenamento do Azure](https://www.azure.com/documentation/services/storage/). Especificamente, discutiremos os seguintes cenários: 
 
-  [Fazer backup e restaurar bancos de dados de/para o armazenamento do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Manter réplicas de banco de dados em máquinas virtuais do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Armazenar arquivos de dados de SQL Server no armazenamento do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Migrar bancos de dados existentes do SQL Server para máquinas virtuais do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Cenários de nuvem híbrida para SQL Server e Microsoft Azure 
 
#### <a name="backup-and-restore-databases-tofrom-azure-storage"></a><a name="backup"></a>Fazer backup e restaurar bancos de dados de/para o armazenamento do Azure 
 Uma das tarefas mais importantes de administrador é fazer backup e restaurar os bancos de dados. Com o SQL Server e o Azure, você pode fazer backup de seus bancos de dados na nuvem com segurança. 
 
 Os principais benefícios de usar os recursos de backup e restauração do SQL Server com o armazenamento do Azure como um destino de backup incluem: 
 
-  Armazenamento de baixo custo ilimitado 
 
-  Armazenamento de alta disponibilidade (replicado geograficamente para garantir que não ocorra nenhuma perda de dados) 
 
-  Armazenamento off-line que pode oferecer suporte aos requisitos de recuperação de desastres e de conformidade 
 
-  Processamento remoto simplificado de backup e restauração 
 
 Veja a seguir a lista de recursos de backup e restauração do SQL Server para cenários de nuvem e locais: 
 
-  O recurso [SQL Server Backup para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) permite que você faça backup no armazenamento do Azure ESPECIFICANDO a URL como o destino de backup. Com este recurso, você pode realizar um backup manual ou configurar manualmente sua própria estratégia de backup, como faria em um armazenamento local ou em outras opções fora do local. 
 
-  O recurso de [criptografia de backup](../relational-databases/backup-restore/backup-encryption.md) permite que você criptografe os dados ao criar um backup para seus destinos de armazenamento: local e armazenamento do Azure. 
 
-  O recurso de [compactação de backup (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) permite que você crie um backup, que é menor do que um backup descompactado dos mesmos dados. A compactação de um backup precisa de menos operações de E/S do dispositivo e, em virtude disso, normalmente aumenta significativamente a velocidade. Isso pode trazer grandes benefícios ao armazenar arquivos de backup no armazenamento do Azure. 
 
-  O recurso [backup gerenciado SQL Server para o Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) permite que você faça o backup automático de bancos de dados SQL Server no [armazenamento do Azure](https://www.azure.com/documentation/services/storage/). Com este recurso, você pode configurar o SQL Server para gerenciar a estratégia de backup e agendar backups para um único banco de dados ou vários bancos de dados, ou defina valores padrão no nível da instância. 
 
-  A [ferramenta SQL Server Backup para o Azure](https://www.microsoft.com/download/details.aspx?id=40740) permite o backup no armazenamento de BLOBs do Azure e criptografa e compacta SQL Server backups armazenados localmente ou na nuvem. Essa ferramenta habilita uma estratégia de backup de nuvem única para várias versões do SQL Server, como o SQL Server 2005, 2008, 2008 R2, e 2014. 
 
#### <a name="maintain-database-replicas-on-azure-virtual-machines"></a><a name="replica"></a>Manter réplicas de banco de dados em máquinas virtuais do Azure 
 Ter uma solução de recuperação de desastre estável para seus bancos de dados é essencial para o sucesso de sua empresa. A maioria dos clientes precisam configurar um site de recuperação de desastres e comprar o hardware adicional para réplicas de banco de dados. Com o SQL Server e o Azure, você pode manter uma ou mais réplicas de seus bancos de dados na nuvem. 
 
 Os principais benefícios da manutenção de réplicas secundárias no Azure incluem: 
 
-  Solução de recuperação de desastres de baixo custo 
 
-  Failover transparente de aplicativo 
 
-  Réplicas disponíveis para descarregar cargas de trabalho e backups de leitura 
 
 Você pode manter réplicas secundárias no Azure usando qualquer uma das seguintes técnicas: 
 
-  O [Assistente para adicionar réplica do Azure](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) permite que você implante uma ou mais réplicas de seus bancos de dados em uma máquina virtual no Azure para recuperação de desastre. 
 
-  Grupos de Disponibilidade AlwaysOn, o espelhamento de banco de dados e o envio de logs são as tecnologias mais comuns que você pode usar para atender às necessidades de alta disponibilidade e recuperação de desastres do seu aplicativo. Para obter informações, consulte [alta disponibilidade e recuperação de desastre para SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store-sql-server-data-files-in-azure-storage"></a><a name="store"></a>Armazenar arquivos de dados de SQL Server no armazenamento do Azure 
 Armazenar arquivos de dados de SQL Server locais no armazenamento do Azure fornece um armazenamento externo flexível, confiável e ilimitado para seus bancos de dados. A partir do SQL Server 2014, você pode usar [SQL Server arquivos de dados no Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) para armazenar SQL Server arquivos de banco de dados no armazenamento do Azure. Com esse recurso, você pode mover arquivos de dados e de log do banco de dados local para o armazenamento do Azure, mantendo o nó de computação do SQL Server em execução no local. Esse recurso permite que você tenha capacidade de armazenamento ilimitada no armazenamento do Azure. 
 
 Os principais benefícios de armazenar arquivos de dados SQL Server armazenamento do Azure incluem: 
 
-  Armazenamento ilimitado de baixo custo no armazenamento do Azure 
 
-  Mais adequado para o descarregamento de cargas de trabalho de leitura de histórico na nuvem para oferecer suporte a aplicativos locais de geração de relatórios 
 
-  Facilita a recuperação de desastres separando a instância de cálculo (uma instância do SQL Server) e os dados (arquivos de dados do SQL Server). Isso permite que você anexe facilmente o banco de dados a outra instância do SQL Server em um ambiente local ou em uma máquina virtual do Azure em caso de desastre. 
 
#### <a name="migrate-existing-sql-server-databases-to-azure-virtual-machines"></a><a name="migrate"></a>Migrar bancos de dados existentes do SQL Server para máquinas virtuais do Azure 
 A computação de nuvem traz alguns benefícios importantes para as empresas, como recursos virtualizados ilimitados disponíveis para você em uma base de pagamento por uso, você pode se beneficiar dos data centers de nuvem públicos em vez de criar e gerenciar seus próprios data centers e, portanto, você pode reduzir custos de TI e de hardware. 
 
 Com [SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/azure/jj823132.aspx), você pode mover os aplicativos locais existentes para o Azure com pouca ou nenhuma alteração de código. Os administradores e desenvolvedores ainda podem usar as mesmas ferramentas de desenvolvimento e administração que estão disponíveis localmente. 
 
 Mover um banco de dados do SQL Server local para SQL Server em execução em uma máquina virtual do Azure normalmente usa um destes caminhos: 
 
-  **Movendo apenas o banco de dados:** Há várias ferramentas e técnicas disponíveis para mover bancos de dados locais existentes para SQL Server em máquinas virtuais do Azure. Para obter diretrizes e recomendações sobre a migração para SQL Server em máquinas virtuais do Azure, consulte [preparando-se para migrar para SQL Server em máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn133142.aspx) e também [migrando para o SQL Server em uma máquina virtual do Azure](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   Além disso, a partir do SQL Server 2014, um novo assistente, [implantar um banco de dados SQL Server em uma máquina virtual Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) está disponível para que você implante o banco de dados em outra instância do SQL Server em execução em uma máquina virtual do Azure. 
 
-  **Movendo a máquina virtual inteira:** Você pode colocar seu próprio SQL Server máquinas virtuais no Azure ou criar uma usando a imagem da plataforma. Em seguida, você pode carregar e anexar um disco de dados que já contém dados à máquina virtual, ou anexar um disco vazio à máquina. Ter uma SQL Server instância de dados em máquinas virtuais do Azure com discos de dados anexados fornece outro armazenamento persistente para seus arquivos de dados e dados de aplicativo. Para obter informações abrangentes e instruções, consulte [SQL Server implantação em máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn133141.aspx). 
 
 Se você planeja mover as camadas de aplicativo (como a camada de apresentação, a camada de negócios e a camada de banco de dados) para as máquinas virtuais do Azure, recomendamos que você examine as recomendações fornecidas nos [padrões de aplicativo e nas estratégias de desenvolvimento para SQL Server no artigo de máquinas virtuais do Azure](https://msdn.microsoft.com/library/dn574746.aspx) . O objetivo deste artigo é fornecer aos desenvolvedores e arquitetos de soluções a base para uma boa arquitetura e design de aplicativos que eles possam seguir ao migrar aplicativos existentes para o Azure, bem como ao desenvolver novos aplicativos no Azure. Para cada padrão do aplicativo, o artigo descreve um cenário local, sua respectiva solução de nuvem habilitada, e as técnicas e recomendações relacionadas. Além disso, o artigo discute estratégias de desenvolvimento específicas do Azure para que você possa criar seus aplicativos corretamente. 
 
## <a name="see-also"></a>Confira também 
 [Guia de produto do SQL Server 2014 CTP2](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Série de blogs de nuvem híbridos do Microsoft SQL Server](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [Migrando aplicativos centrados em dados para o Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
