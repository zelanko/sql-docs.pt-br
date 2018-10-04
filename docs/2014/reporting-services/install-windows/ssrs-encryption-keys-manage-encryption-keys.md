---
title: Configurar e gerenciar chaves de criptografia (	Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16a1851a46b6602bc9d92d5c7e0111ece8701d43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222506"
---
# <a name="configure-and-manage-encryption-keys-ssrs-configuration-manager"></a>Configurar e gerenciar chaves de criptografia (Gerenciador de configurações do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa chaves de criptografia para proteger credenciais e informações de conexão que estão armazenadas em um banco de dados de servidor de relatório. No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o suporte à criptografia é dado por meio de uma combinação de chaves públicas, privadas e simétricas, usadas para proteger dados confidenciais. A chave simétrica é criada durante a inicialização do servidor de relatório quando você instala ou configura o servidor de relatório, sendo usada pelo servidor de relatório para criptografar dados confidenciais que estão armazenados no servidor de relatório. As chaves públicas e privadas são criadas pelo sistema operacional e são usadas para proteger a chave simétrica. Um par de chaves pública e privada é criado para cada instância do servidor de relatório, que armazena dados confidenciais em um banco de dados de servidor de relatório.  
  
 O gerenciamento das chaves de criptografia consiste na criação de uma cópia de backup da chave simétrica, além de saber quando e como restaurar, excluir ou alterar as chaves. Se você migrar a instalação de um servidor de relatório ou configurar uma implantação de expansão, deverá ter uma cópia de backup da chave simétrica, de maneira que seja possível aplicá-la à nova instalação.  
  
> [!IMPORTANT]  
>  Alterar periodicamente a chave de criptografia do Reporting Services é uma prática recomendada de segurança. Um momento indicado para alterar a chave é imediatamente após uma atualização de versão principal do Reporting Services. Alterar a chave depois de uma atualização minimiza a interrupção de serviço adicional causada pela alteração da chave de criptografia do Reporting Services fora do ciclo de atualização.  
  
 Para gerenciar chaves simétricas, você pode usar a ferramenta Configuração do Reporting Services ou o utilitário **rskeymgmt** . As ferramentas incluídas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são usadas para gerenciar somente a chave simétrica (as chaves pública e privada são gerenciadas pelo sistema operacional). A ferramenta Configuração do Reporting Services e o utilitário **rskeymgmt** dão suporte às seguintes tarefas:  
  
-   Fazer o backup de uma cópia da chave simétrica, para que você possa usá-la para recuperar a instalação de um servidor de relatório ou como parte de uma migração planejada.  
  
-   Restaurar uma chave simétrica salva anteriormente para um banco de dados de servidor de relatório, permitindo que uma nova instância do servidor de relatório acesse dados existentes que ele não criptografou originalmente.  
  
-   Excluir os dados criptografados em um banco de dados de servidor de relatório no caso improvável de que você não mais possa acessar os dados criptografados.  
  
-   Recriar chaves simétricas e criptografar novamente os dados no caso improvável de que a chave simétrica seja comprometida. Como prática recomendável de segurança, você deve recriar a chave simétrica periodicamente (por exemplo, a cada tantos meses) a fim de proteger o banco de dados do servidor de relatório contra ataques cibernéticos que tentem decifrar a chave.  
  
-   Adicionar ou remover uma instância do servidor de relatório de uma implantação de expansão do servidor de relatório em que vários servidores de relatório compartilham um único banco de dados de servidor de relatório e a chave simétrica que fornece criptografia reversível para esse banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Inicializar um servidor de relatório &#40;Configuration Manager do SSRS&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
 Explica como as chaves de criptografia são criadas.  
  
 [Fazer backup e restaurar as chaves de criptografia do Reporting Services](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 Explica como fazer o backup de chaves de criptografia e restaurá-las para recuperar ou migrar uma instalação de servidor de relatório.  
  
 [Dados do servidor de relatório criptografado de Store &#40;Configuration Manager do SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 Descreve criptografia em um servidor de relatório.  
  
 [Excluir e recriar chaves de criptografia &#40;Configuration Manager do SSRS&#41;](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 Explica como é possível substituir uma chave simétrica por uma nova versão e como iniciar do princípio se as chaves simétricas não puderem ser validadas.  
  
 [Adicionar e remover chaves de criptografia para implantação escalável &#40;Configuration Manager do SSRS&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 Explica como adicionar e remover chaves de criptografia para controlar quais servidores de relatório fazem parte de uma implantação de expansão.  
  
## <a name="see-also"></a>Consulte também  
 [Dados do servidor de relatório criptografado de Store &#40;Configuration Manager do SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
