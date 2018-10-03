---
title: Dispositivo de backup (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a4f23fd3d6d8208410c520676ee4e0c8bbe00fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140686"
---
# <a name="backup-device-general-page"></a>Dispositivo de backup (página Geral)
  Use a página **Geral** para especificar ou exibir as propriedades gerais de um dispositivo de backup lógico.  
  
 **Para usar o SQL Server Management Studio para exibir o conteúdo de um dispositivo de backup**  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opções  
 **Nome de dispositivo**  
 Exibe o nome de um dispositivo de backup lógico existente ou especifica o nome de um novo dispositivo de backup lógico.  
  
 **Tape**  
 Exibe ou seleciona o dispositivo de fita de destino na lista **Fita** . Essa opção estará disponível apenas se uma unidade de fita for anexada ao computador que está executando a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  Dispositivos de backup em fita em computadores remotos não são destinos de backup válidos.  
  
 **File**  
 Exibe o arquivo de destino de um dispositivo de backup lógico existente ou especifica um arquivo de destino para um novo dispositivo de backup lógico.  
  
-   O caminho do arquivo de backup é exibido para um dispositivo de backup lógico existente. O campo **Arquivo** não é editável e o botão Procurar está indisponível.  
  
-   Para um novo dispositivo de backup lógico, você deve fornecer o caminho do arquivo de backup para o qual está definindo o dispositivo de backup lógico. Esse arquivo não precisa existir ainda.  
  
     Para especificar um arquivo de backup local, você pode clicar no botão Procurar à direita da caixa de texto **Arquivo** . Então, na caixa de diálogo **Localizar Arquivos de Bancos de Dados** , será possível navegar para o local em unidades fixas no computador que executa a instância de servidor. Se o arquivo de backup ainda não existir, você deve digitar o nome de arquivo que deseja usar no campo **Nome do arquivo** da caixa de diálogo.  
  
     Como alternativa,´você pode editar o campo **Arquivo** manualmente para anular o caminho, nome de arquivo e extensão padrão. Para especificar um arquivo remoto como seu destino de backup, digite o nome da Convenção Universal de Nomenclatura (UNC) totalmente qualificada. Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Backups de dados em uma rede podem estar sujeitos a erros de rede; assim, recomendamos que você verifique a operação de backup quando ela estiver concluída. Para obter mais informações, consulte [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
## <a name="remarks"></a>Comentários  
 Os backups em um conjunto de um ou mais dispositivos de backup compõem um único conjunto de mídias. Um *conjunto de mídias* é uma coleção ordenada de mídias de backup, fitas ou arquivos de disco, em que uma ou mais operações de backup foram gravadas, usando um número e tipo fixo de dispositivos de backup. Para obter informações sobre conjuntos de mídias, consulte [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 O dispositivo de backup físico, que corresponde a um dispositivo de backup lógico, é inicializado quando o primeiro backup no conjunto de mídia é escrito ao dispositivo de backup lógico. Se o dispositivo de backup físico for um arquivo que ainda não existe, ele será criado nesse momento.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Excluir um dispositivo de backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Definir a data de validade em um backup &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir os dados e arquivos de log em um conjunto de backup &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
