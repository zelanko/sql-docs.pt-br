---
title: Introdução à nuvem híbrida do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fc36b9e907a9399a47b2d4f3a743e3f83bfa7a31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005709"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introdução à nuvem híbrida do SQL Server 2014
 A maioria dos aplicativos têm alguns desafios principais, como a alta eficiência, valor comercial, configurações de hardware complexas, picos maciços sob demanda, e a conformidade com a indústria e os regulamentos corporativos. Considerando que todos esses fatores e a criação de uma tecnologia a nível empresarial possam ser muito desafiadores. A estratégia de nuvem híbrida da Microsoft oferece suporte para a nuvem tradicional, nuvem particular, nuvem pública, e os ambientes de nuvem híbridos para superar esses desafios fundamentais. 
 
 Quando sua empresa exige uma infraestrutura de TI flexível que pode ser dimensionada sob demanda, você pode criar uma nuvem privada em seu data center ou em uma nuvem pública nos centros de dados globais do Azure. Quando você estende o data center para localizar a nuvem pública, você cria um modelo de nuvem híbrido. 
 
 Este tópico apresenta os recursos do SQL Server 2014 que suportam cenários de nuvem híbrida. Para obter informações detalhadas sobre a estratégia de nuvem híbrida da Microsoft e o SQL Server, consulte o site [TI híbrida do SQL Server](http://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, o Azure e a nuvem híbrida 
 Usando as tecnologias da Microsoft, você pode executar o código localmente ou na nuvem, executar na nuvem usando dados locais, ou executar totalmente na nuvem usando mais de um data center. Portanto, você pode mover seus aplicativos para a nuvem em seu próprio local enquanto preserva o valor dos investimentos de TI herdade. 
 
 Neste artigo, nosso foco nos cenários de nuvem híbrida que abrangem do SQL Server no local até as ofertas de nuvem pública do Azure: [do SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/azure/jj823132.aspx) e [armazenamento do Azure](http://www.azure.com/documentation/services/storage/). Discutiremos especificamente os seguintes cenários: 
 
-  [Backup e restaurar bancos de dados para/do armazenamento do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Manter réplicas de banco de dados em máquinas virtuais do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Armazenar arquivos de dados do SQL Server no armazenamento do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Migrar bancos de dados do SQL Server existentes para máquinas virtuais do Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Cenários de nuvem híbrida do SQL Server e do Microsoft Azure 
 
#### <a name="backup"></a> Backup e restaurar bancos de dados para/do armazenamento do Azure 
 Uma das tarefas mais importantes de administrador é fazer backup e restaurar os bancos de dados. Com o SQL Server e do Azure, você pode seguramente fazer backup de seus bancos de dados na nuvem. 
 
 Os principais benefícios do uso dos recursos de backup e restauração do SQL Server com armazenamento do Azure como um destino de backup incluem: 
 
-  Armazenamento de baixo custo ilimitado 
 
-  Armazenamento de alta disponibilidade (replicado geograficamente para garantir que não ocorra nenhuma perda de dados) 
 
-  Armazenamento off-line que pode oferecer suporte aos requisitos de recuperação de desastres e de conformidade 
 
-  Processamento remoto simplificado de backup e restauração 
 
 Veja a seguir a lista de recursos de backup e restauração do SQL Server para cenários de nuvem e locais: 
 
-  O [Backup do SQL Server para URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) recurso permite que você faça backup no armazenamento do Azure, especificando a URL como destino de backup. Com este recurso, você pode realizar um backup manual ou configurar manualmente sua própria estratégia de backup, como faria em um armazenamento local ou em outras opções fora do local. 
 
-  O [criptografia de Backup](../relational-databases/backup-restore/backup-encryption.md) recurso permite que você criptografe os dados durante a criação de um backup para os destinos de armazenamento: local e o armazenamento do Azure. 
 
-  O [compactação de Backup (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) recurso permite que você crie um backup, que é menor do que um backup não compactado dos mesmos dados. A compactação de um backup precisa de menos operações de E/S do dispositivo e, em virtude disso, normalmente aumenta significativamente a velocidade. Isso pode trazer grandes benefícios ao armazenar os arquivos de backup no armazenamento do Azure. 
 
-  O [Backup gerenciado do SQL Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) recurso permite backup automaticamente bancos de dados do SQL Server para [armazenamento do Azure](http://www.azure.com/documentation/services/storage/). Com este recurso, você pode configurar o SQL Server para gerenciar a estratégia de backup e agendar backups para um único banco de dados ou vários bancos de dados, ou defina valores padrão no nível da instância. 
 
-  O [Backup do SQL Server para a ferramenta Azure](http://www.microsoft.com/download/details.aspx?id=40740) permite fazer backup no armazenamento de BLOBs do Azure e criptografar e compactar os backups do SQL Server armazenados localmente ou na nuvem. Essa ferramenta habilita uma estratégia de backup de nuvem única para várias versões do SQL Server, como o SQL Server 2005, 2008, 2008 R2, e 2014. 
 
#### <a name="replica"></a> Manter réplicas de banco de dados em máquinas virtuais do Azure 
 Ter uma solução estável de recuperação de desastres para seus bancos de dados é essencial para seu êxito comercial. A maioria dos clientes precisam configurar um site de recuperação de desastres e comprar o hardware adicional para réplicas de banco de dados. Com o SQL Server e do Azure, você pode manter uma ou mais réplicas de bancos de dados na nuvem. 
 
 Os principais benefícios de manter réplicas secundárias no Azure incluem: 
 
-  Solução de recuperação de desastres de baixo custo 
 
-  Failover transparente de aplicativo 
 
-  Réplicas disponíveis para descarregar cargas de trabalho e backups de leitura 
 
 Você pode manter réplicas secundárias no Azure, usando qualquer uma das seguintes técnicas: 
 
-  O [assistente Adicionar réplica do Azure](http://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) permite que você implante uma ou mais réplicas de seus bancos de dados para uma máquina virtual no Azure para recuperação de desastres. 
 
-  Os grupos de disponibilidade AlwaysOn, o espelhamento de banco de dados, e o envio de logs são as tecnologias mais comuns que você pode usar para resolver as necessidades de alta disponibilidade e de recuperação de desastre do seu aplicativo. Para obter informações, consulte [alta disponibilidade e recuperação de desastres do SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store"></a> Armazenar arquivos de dados do SQL Server no armazenamento do Azure 
 Armazenar arquivos de dados local do SQL Server no armazenamento do Azure fornece um armazenamento externo flexível, confiável e ilimitado para seus bancos de dados. Começando com o SQL Server 2014, você pode usar [arquivos de dados do SQL Server no Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) para armazenar arquivos de banco de dados do SQL Server no armazenamento do Azure. Com esse recurso, você pode mover dados e arquivos de log do banco de dados local para o armazenamento do Azure, mantendo o nó de computação do SQL Server em execução no local. Esse recurso permite que você tenha a capacidade de armazenamento ilimitado no armazenamento do Azure. 
 
 Os principais benefícios de armazenar arquivos de dados do SQL Server o armazenamento do Azure incluem: 
 
-  Armazenamento de baixo custo ilimitado no armazenamento do Azure 
 
-  Mais adequado para o descarregamento de cargas de trabalho de leitura de histórico na nuvem para oferecer suporte a aplicativos locais de geração de relatórios 
 
-  Facilita a recuperação de desastres separando a instância de cálculo (uma instância do SQL Server) e os dados (arquivos de dados do SQL Server). Isso permite anexar facilmente o banco de dados para outra instância do SQL Server em um ambiente local ou em uma máquina virtual do Azure em caso de desastre. 
 
#### <a name="migrate"></a> Migrar bancos de dados do SQL Server existentes para máquinas virtuais do Azure 
 A computação de nuvem traz alguns benefícios importantes para as empresas, como recursos virtualizados ilimitados disponíveis para você em uma base de pagamento por uso, você pode se beneficiar dos data centers de nuvem públicos em vez de criar e gerenciar seus próprios data centers e, portanto, você pode reduzir custos de TI e de hardware. 
 
 Com [do SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/azure/jj823132.aspx), você pode mover os aplicativos locais existentes para o Azure com pouca ou nenhuma alteração de código. Os administradores e desenvolvedores ainda podem usar as mesmas ferramentas de desenvolvimento e administração que estão disponíveis localmente. 
 
 Mover um banco de dados do SQL Server no local para o SQL Server em execução em uma máquina Virtual do Azure normalmente usa um desses caminhos: 
 
-  **Mover apenas o banco de dados:** existem várias ferramentas e técnicas disponíveis para mover o local existente bancos de dados do SQL Server em máquinas virtuais do Azure. Para obter diretrizes e recomendações sobre a migração para o SQL Server em máquinas virtuais do Azure, consulte [Preparando-se para migrar para o SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/dn133142.aspx) e também [migrando para o SQL Server em uma máquina Virtual do Azure ](http://msdn.microsoft.com/library/jj156165.aspx). 
 
   Além disso, começando com o SQL Server 2014, um novo assistente, [implantar um banco de dados do SQL Server para uma máquina Virtual Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) está disponível para implantar o banco de dados para outra instância do SQL Server em execução em uma máquina Virtual do Azure. 
 
-  **Movendo a máquina virtual inteira:** você pode colocar suas próprias máquinas virtuais de SQL Server no Azure ou criar um usando a imagem da plataforma. Em seguida, você pode carregar e anexar um disco de dados que já contém dados à máquina virtual, ou anexar um disco vazio à máquina. Ter uma instância de dados do SQL Server em máquinas virtuais do Azure com discos de dados anexados fornece outro repositório persistente para seus arquivos de dados e dados de aplicativo. Para obter informações abrangentes e tutoriais, consulte [implantação do SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/dn133141.aspx). 
 
 Se você planeja mover as camadas de aplicativo (por exemplo, a camada de apresentação, a camada de negócios e a camada de banco de dados) para as máquinas virtuais do Azure, recomendamos que você examine as recomendações fornecidas no [padrões de aplicativo e desenvolvimento Estratégias para o SQL Server em máquinas virtuais Azure](http://msdn.microsoft.com/library/dn574746.aspx) artigo. O objetivo deste artigo é fornecer uma base de desenvolvedores e arquitetos de solução para aplicativo boa arquitetura e design, qual eles podem seguir ao migrar aplicativos existentes para o Azure, bem como desenvolver novos aplicativos no Azure. Para cada padrão do aplicativo, o artigo descreve um cenário local, sua respectiva solução de nuvem habilitada, e as técnicas e recomendações relacionadas. Além disso, o artigo discute estratégias de desenvolvimento específicas do Azure para que você possa criar seus aplicativos corretamente. 
 
## <a name="see-also"></a>Confira também 
 [Guia de produto do SQL Server 2014 CTP2](http://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](http://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Série de Blog de nuvem do Microsoft SQL Server híbrido](http://blogs.msdn.com/b/azure/archive/2013/10/16/microsoft-sql-server-hybrid-cloud-blog-series.aspx)  
 [Migrando aplicativos centrados em dados para o Azure](http://msdn.microsoft.com/library/jj156154.aspx) 
 
 