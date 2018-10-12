---
title: Serviço Gravador do SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- VDI [SQL Server]
- restoring [SQL Server], SQL Writer Service
- backups [SQL Server], while SQL Server running
- Volume Shadow Copy Service
- volume backups while running [SQL Server]
- Virtual Backup Device Interface [SQL Server]
- SQL Writer Service
- services [SQL Server], SQL Writer
- MSDE Writer
- VSS
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 80eb04dfefca7903592ea391d915e140d93f479f
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888342"
---
# <a name="sql-writer-service"></a>Serviço do gravador do SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Serviço Gravador do SQL oferece funcionalidade adicional para fazer backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio da estrutura do Serviço de Cópias de Sombra de Volume.  
  
 O Serviço Gravador do SQL é instalado automaticamente. Deve estar em execução quando o aplicativo VSS (Volume Shadow Copy Service) pedir um backup ou uma restauração. Para configurar o serviço, use o miniaplicativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] do Windows Services. O Serviço Gravador do SQL é instalado em todos os sistemas operacionais.  
  
## <a name="purpose"></a>Finalidade  
 Quando está em execução, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] bloqueia os arquivos de dados e tem acesso exclusivo a eles. Quando o Serviço Gravador do SQL não está em execução, os programas de backup em execução no Windows não têm acesso aos arquivos de dados e os backups devem ser executados usando o backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Use o Serviço Gravador do SQL para permitir que os programas de backup do Windows copiem arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando.  
  
## <a name="volume-shadow-copy-service"></a>Serviço de cópias de sombra de volume  
 O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir que backups dos volumes sejam feitos enquanto os aplicativos em um sistema continuam a gravar nos volumes. O VSS oferece uma interface consistente que permite a coordenação entre os aplicativos de usuário que atualizam dados em disco (gravadores) e os aplicativos de backup (solicitantes).  
  
 O VSS captura e copia imagens estáveis para backup em sistemas em execução, particularmente servidores, sem degradar indevidamente o desempenho e a estabilidade dos serviços que oferecem. Para obter mais informações sobre o VSS, consulte sua documentação do Windows.  

> [!NOTE]
> Ao usar o VSS para fazer backup de uma máquina virtual que esteja hospedando um Grupo de Disponibilidade Básico, se a máquina virtual estiver hospedando bancos de dados em um estado secundário, a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU9 *não* será feito o backup desses bancos de dados com a máquina virtual.  Isso ocorre porque os Grupos de Disponibilidade Básicos não oferecem suporte para backup de bancos de dados na réplica secundária.  Antes dessas versões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o backup falhará apresentando um erro.
  
## <a name="virtual-backup-device-interface-vdi"></a>VDI (Virtual Backup Device Interface)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece uma API chamada VDI que permite que fornecedores de software independente integrem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seus produtos para dar suporte a operações de backup e restauração. Essas APIs são criadas para prover confiabilidade e desempenho máximos, e dão suporte a todas as funcionalidades de backup e de restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive todas as capacidades de backup hot e instantâneo.  
  
## <a name="permissions"></a>Permissões  
 O Serviço Gravador do SQL deve ser executado na conta **Sistema Local** . O Serviço Gravador do SQL usa o logon **NT Service\SQLWriter** para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O uso do logon **NT Service\SQLWriter** permite que o processo do Gravador do SQL seja executado no nível mais baixo de privilégio em uma conta designada como **nenhum logon**, que limita a vulnerabilidade. Se o serviço do Gravador do SQL estiver desabilitado, qualquer utilitário que confie em instantâneos do VSS, como o System Center Data Protection Manager, bem como em outros produtos de terceiros, será interrompido, ou pior, correrá o risco de obter backups de bancos de dados que não estavam consistentes. Se nem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o sistema em que é executado, nem o sistema host (no caso de uma máquina virtual), precisarem usar qualquer coisa além do backup de [!INCLUDE[tsql](../../includes/tsql-md.md)] , o serviço do Gravador do SQL poderá seguramente ser desabilitado e o logon será removido.  Observe que o serviço do Gravador do SQL pode ser chamado por um backup em nível de sistema ou de volume, seja o backup diretamente baseado em instantâneo ou não. Alguns produtos de backup de sistema usam o VSS para evitar serem bloqueados por arquivos abertos ou bloqueados. O Serviço Gravador do SQL precisa de permissões elevadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pois, no decorrer de suas atividades, ele congelará brevemente qualquer E/S para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="features"></a>Recursos  
 O Gravador do SQL dá suporte a:  
  
-   Backup e restauração de banco de dados completos inclusive catálogos de texto completo  
  
-   Backup diferencial e restauração  
  
-   Restaurar e mover  
  
-   Renomear banco de dados  
  
-   Backup somente cópia  
  
-   Recuperação automática de instantâneo do banco de dados  
  
 O Gravador do SQL não dá suporte a:  
  
-   Backups de log  
  
-   Backup de arquivo e grupo de arquivos  
  
-   Restauração de página  
  
## <a name="remarks"></a>Remarks
O serviço Gravador do SQL é um serviço separado do mecanismo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sendo compartilhado entre diferentes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e entre diferentes instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mesmo servidor.  O arquivo do serviço Gravador do SQL é fornecido como parte do pacote de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e será marcado com o mesmo número de versão que o mecanismo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornecido com ele.  Quando uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalada em um servidor ou uma instância existente é atualizada, se o número de versão da instância que está sendo instalada ou atualizada for maior do que o número de versão do serviço Gravador do SQL que está no servidor no momento, esse arquivo será substituído por um do pacote de instalação.  Se o Serviço Gravador do SQL tiver sido atualizado por um Service Pack ou por Atualização cumulativa e uma versão RTM do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo instalada, será possível substituir uma versão mais recente do Serviço Gravador do SQL por uma mais antiga, desde que a instalação tenha um número de versão principal maior.  Por exemplo, o Serviço Gravador do SQL foi atualizado no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2.  Se essa instância for atualizada para [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] RTM, o Gravador do SQL atualizado será substituído por uma versão mais antiga.  Nesse caso, você precisaria aplicar a CU mais recente à nova instância para obter a versão mais nova do serviço do Gravador do SQL.

