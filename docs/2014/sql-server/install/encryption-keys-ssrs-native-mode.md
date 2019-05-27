---
title: As chaves de criptografia (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16ac264f89c541f0a864f8b47ed008fa254f181c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095422"
---
# <a name="encryption-keys-ssrs-native-mode"></a>Chaves de Criptografia (modo nativo do SSRS)
  Use a página Chaves de Criptografia para gerenciar a chave simétrica usada para criptografar e descriptografar dados em um servidor de relatório. O gerenciamento das chaves de criptografia é uma parte importante da configuração do servidor de relatório. A chave simétrica é criada e aplicada automaticamente quando você cria o banco de dados do servidor de relatórios. Crie uma cópia de backup da chave simétrica de modo que você possa executar operações de manutenção rotineiras. As seguintes tarefas de manutenção requerem que você tenha uma cópia válida da chave simétrica:  
  
-   Alterar a conta de serviço para o serviço Servidor de Relatório.  
  
-   Migrar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um computador diferente.  
  
-   Configurar uma nova instância de servidor de relatório para compartilhar ou usar um banco de dados de servidor de relatório existente.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Alterar periodicamente a chave de criptografia do Reporting Services é uma prática recomendada de segurança. Um momento indicado para alterar a chave é imediatamente após uma atualização de versão principal do Reporting Services. Alterar a chave depois de uma atualização minimiza a interrupção de serviço adicional causada pela alteração da chave de criptografia do Reporting Services fora do ciclo de atualização.  
  
 A restauração da chave simétrica será necessária se você tiver atualizado a conta de usuário do serviço Servidor de Relatório (e usado uma ferramenta que não seja o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para alterar a conta), ou se estiver migrando uma instalação do servidor de relatório para um novo servidor.  
  
 Para proteger a chave simétrica contra acesso não autorizado, a chave simétrica é criptografada usando a chave privada do serviço Servidor de Relatório. Somente o serviço Servidor de Relatório pode desbloquear e usar a chave simétrica para armazenar dados confidenciais no banco de dados do servidor de relatório. Se você alterar a identidade do serviço Servidor de Relatório ou migrar o servidor de relatório para um novo computador, a chave privada do serviço Servidor de Relatório não mais poderá desbloquear a chave simétrica. Para restaurar o acesso à chave simétrica, criptografe novamente a chave simétrica usando a chave privada da nova identidade do serviço Servidor de Relatório. A restauração da chave simétrica é o processo pelo qual a recriptografia ocorre.  
  
 Somente restaure uma chave simétrica se ela for a mesma chave utilizada atualmente para criptografar e descriptografar dados no banco de dados do servidor de relatório. Se você restaurar uma chave simétrica que não seja válida, não poderá mais acessar os dados confidenciais. Nesse caso, exclua e recrie a chave.  
  
> [!IMPORTANT]  
>  A ação de excluir e recriar a chave simétrica não pode ser invertida ou desfeita. Excluir ou recriar a chave simétrica pode ter ramificações importantes em sua instalação atual. Se você excluir a chave, quaisquer dados existentes criptografados pela chave simétrica também serão excluídos. Os dados excluídos incluem cadeias de caracteres de conexão a fontes de dados de relatório externas, cadeias de caracteres de conexões armazenadas e algumas informações de assinatura.  
  
 Para abrir essa página, inicie o Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selecione o link no painel de navegação. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opções  
 **Backup**  
 Copia a chave simétrica para um arquivo que você especificar. A chave simétrica nunca é armazenada em texto sem-formatação. Você deve digitar uma senha para proteger o arquivo.  
  
 **Restaurar**  
 Aplica uma cópia previamente salva da chave simétrica ao banco de dados do servidor de relatório. Você deve fornecer a senha para desbloquear o arquivo.  
  
 A cópia anterior da chave simétrica para a instância do servidor de relatório à qual você está conectado atualmente será substituída pela versão restaurada. Depois que você restaurar a chave simétrica, deverá inicializar todos os servidores de relatório que usam o banco de dados do servidor de relatório. Para obter mais informações sobre como inicializar servidores de relatório, consulte [inicializar um servidor de relatório &#40;Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
 **Alteração**  
 Recria a chave simétrica e recriptografa todos os valores criptografados no banco de dados do servidor de relatório. Pare o serviço Servidor de Relatório antes de recriar a chave simétrica.  
  
 Em uma implantação de expansão, todas as cópias da chave simétrica serão substituídas por versões mais novas. Antes de alterar a chave simétrica, revise a lista de servidores que estão associados à implantação de expansão para verificar que somente instâncias válidas do servidor de relatório recebam acesso à nova chave. Os servidores que fazem parte de uma implantação de expansão são listados na página **Implantação de Expansão** . Pare o serviço em cada servidor de relatório na implantação antes de recriar a chave.  
  
 Observe que a regeneração da chave simétrica pode ser um processo longo se você tiver muitas fontes de dados e assinaturas.  
  
 **Delete (excluir)**  
 Exclui a chave simétrica e todo o conteúdo criptografado, incluindo cadeias de caracteres de conexão e credenciais armazenadas. Você somente deve excluir a chave simétrica se não puder restaurá-la.  
  
 Depois de excluir a chave simétrica, você deve inserir novamente as cadeias de caracteres de conexão e credenciais armazenadas ausentes nos relatórios e fontes de dados compartilhadas que não mais tenham esses valores. Você também deve atualizar todas as assinaturas que usam extensões de entrega que armazenam dados criptografados. Isso inclui a extensão de entrega de compartilhamento de arquivo e qualquer extensão de entrega de terceiros que usem valor criptografado.  
  
 Não há nenhum modo automatizado para atualizar essas informações. Cada relatório, assinatura e fonte de dados compartilhada que use credenciais armazenadas e cadeias de caracteres de conexão deve ser atualizado individualmente.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de Ajuda F1 do Configuration Manager do Reporting Services &#40;modo nativo do SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar um servidor de relatório &#40; Configuration Manager do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
