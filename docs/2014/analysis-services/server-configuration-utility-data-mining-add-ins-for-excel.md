---
title: Utilitário de configuração do servidor (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 28435f86-5cec-4a1e-9b7d-b2069c1ddddb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdc8434673d9220f22d31f1736bd67012653dc88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069066"
---
# <a name="server-configuration-utility-data-mining-add-ins-for-excel"></a>Utilitário de Configuração de Servidor (Suplementos de Mineração de Dados para Excel)
  Quando você instala os suplementos de mineração de dados para Excel, um utilitário de configuração do servidor também é instalado e será executado na primeira vez que você abrir os suplementos. Este tópico descreve como usar o utilitário para se conectar a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e configurar um banco de dados para trabalhar com modelos de data mining.  
  

  
##  <a name="bkmk_step1"></a>Etapa 1: conectar-se ao Analysis Services  
 Escolha o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que fornece os algoritmos de mineração de dados e armazena os modelos de mineração de dados.  
  
 Quando você cria uma conexão para permitir a mineração de dados, é necessário escolher um servidor onde seja possível fazer experiências com modelos de mineração de dados. Recomendamos que você crie um novo banco de dados do servidor e dedique o novo banco de dados da mineração de dados ou peça ao administrador para preparar um servidor de mineração de dados. Dessa forma, você pode criar modelos sem afetar o desempenho de outros serviços.  
  
 Observe que o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você usa para mineração de dados não precisa estar no mesmo servidor da fonte de dados.  
  
 **Nome do servidor**  
 Digite o nome do servidor que contém a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que você usará para mineração de dados.  
  
 **Autenticação**  
 Especifique os métodos de autenticação. A Autenticação do Windows é necessária para conexões com o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], a menos que o administrador tenha configurado o acesso ao servidor por meio de HTTPPump.  
  
##  <a name="bkmk_step2"></a>Etapa 2: permitir modelos temporários  
 Antes de poder usar os suplementos, uma propriedade de servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] deve ser alterada para permitir a criação de modelos de mineração temporários.  
  
 Os modelos de mineração temporários também são chamados de *modelos de sessão*. Isso ocorre porque os modelos são armazenados apenas enquanto a sessão atual permanece aberta. Quando você fecha a conexão com o servidor, a sessão é encerrada e os modelos usados durante ela são excluídos.  
  
 O uso de modelos de mineração de sessão não afeta o espaço de armazenamento no servidor, mas a sobrecarga envolvida na criação de modelos de mineração de dados pode afetar o desempenho do servidor.  
  
 O assistente detecta primeiro as configurações no servidor que você especificou. Se o servidor já permitir modelos de mineração temporários, você poderá clicar em **Avançar** para continuar. O assistente também fornece instruções sobre como habilitar modelos de mineração temporários no servidor especificado do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou como fazer uma solicitação ao administrador do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
##  <a name="bkmk_step3"></a>Etapa 3: criar um banco de dados para usuários do suplemento  
 Nesta página do assistente de instalação e configuração, você pode criar um novo banco de dados dedicado à mineração de dados ou selecionar um banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] existente.  
  
> [!WARNING]  
>  A mineração de dados requer uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em execução no modo multidimensional. O modo de tabela não oferece suporte à mineração de dados.  
  
 É recomendável criar um banco de dados separado dedicado à mineração de dados. Isso lhe permite fazer experiências com modelos de mineração de dados sem afetar outros objetos da solução.  
  
 Se você escolher um banco de dados existente em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], observe que será possível substituir modelos existentes se você usar os suplementos para criar um modelo e já houver um modelo com esse nome.  
  
 **Criar novo banco de dados**  
 Selecione esta opção para criar um novo banco de dados no servidor selecionado. Um banco de dados de mineração de dados armazenará suas fontes de dados, estruturas de mineração e modelos de mineração.  
  
 **Nome do banco de dados**  
 Digite o nome do novo banco de dados. Se o nome ainda não estiver em uso, ele será criado para você.  
  
 **Usar banco de dados existente**  
 Selecione esta opção para usar um banco de dados [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] existente.  
  
 **Backup de banco de dados**  
 Se você escolher a opção de usar um banco de dados existente, selecione o nome desse banco de dados na lista.  
  
##  <a name="bkmk_step4"></a>Etapa 4: conceder permissões apropriadas aos usuários do suplemento  
 Você deve assegurar que você e outros usuários de suplementos tenham as permissões necessárias para procurar, editar, processar ou criar estruturas e modelos de mineração de dados.  
  
 Por padrão, a Autenticação do Windows integrada é necessária para uso dos suplementos.  
  
 **Dar aos usuários de suplementos permissões de administração de banco de dados**  
 Selecione esta opção para dar aos usuários listados acesso administrativo ao banco de dados.  
  
> [!NOTE]  
>  Essas permissões se aplicam somente ao banco de dados listado na caixa **nome do banco de dados** .  
  
 **Nome do banco de dados**  
 Exibe o nome do banco de dados selecionado.  
  
 **Especificar os usuários ou grupos a serem adicionados**  
 Selecione os logons que terão acesso ao banco de dados usado para mineração de dados.  
  
 **Adicionar**  
 Clique para abrir uma caixa de diálogo e adicionar usuários ou grupos.  
  
 **Remover**  
 Clique para remover o usuário ou grupo selecionado na lista de usuários com permissões administrativas.  
  
  
