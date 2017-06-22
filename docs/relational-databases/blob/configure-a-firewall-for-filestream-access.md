---
title: Configurar um firewall para acesso ao FILESTREAM | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbaaa631770966cff9cafa15fffb60b24dcd2767
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-a-firewall-for-filestream-access"></a>Configurar um firewall para acesso ao FILESTREAM
  Para usar FILESTREAM em um ambiente protegido por firewall, o cliente e o servidor devem poder resolver nomes DNS para o servidor que contém os arquivos de FILESTREAM. O FILESTREAM exige que as portas de compartilhamento de arquivos do Windows 139 e 445 estejam abertas.  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>Para abrir as portas de compartilhamento de arquivos do Windows em um computador que está executando o Windows 7  
  
1.  No Painel de Controle, abra o **Firewall do Windows**.  
  
2.  No painel esquerdo, clique em **Configurações avançadas**. Se você for solicitado a fornecer uma senha de administrador ou confirmação, digite a senha ou forneça confirmação.  
  
3.  Na caixa de diálogo **Firewall do Windows com Segurança Avançada** , no painel esquerdo, clique em **Regras de Entrada**e, no painel direito, clique em **Nova Regra**.  
  
4.  Siga as instruções do assistente Nova Regra de Entrada para adicionar a porta TCP 139.  
  
5.  Repita a etapa anterior para adicionar a porta TCP 445.  
  
6.  Feche a caixa de diálogo **Firewall do Windows com Segurança Avançada** .  
  
  
