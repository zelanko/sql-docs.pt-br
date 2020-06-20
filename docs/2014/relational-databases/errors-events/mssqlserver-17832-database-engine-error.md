---
title: MSSQLSERVER_17832 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 245cf55b5cff4cb203b20557d6944e0d05375a99
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967796"
---
# <a name="mssqlserver_17832"></a>MSSQLSERVER_17832
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|17832|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_BAD_LOGIN_PKT|  
|Texto da mensagem|O pacote de logon usado para abrir a conexão é estruturalmente inválido; a conexão foi fechada. Contate o fornecedor da biblioteca de cliente.%. * ls|  
  
## <a name="explanation"></a>Explicação  
 O computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde processar o pacote de logon do cliente. Talvez isso ocorra porque o pacote foi criado de modo inadequado ou porque foi danificado durante a transmissão. Também pode ocorrer devido à configuração do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O endereço IP listado é o endereço do computador cliente.  
  
### <a name="more-information"></a>Mais informações  
 Ao usar a Autenticação Windows em um ambiente Kerberos, um cliente recebe um tíquete Kerberos que contém um Certificado de Atributos de Privilégio (PAC). O PAC contém vários tipos de dados de autorização, inclusive grupos dos quais o usuário é membro, direitos que o usuário possui e quais políticas se aplicam ao usuário. Quando o cliente recebe o tíquete Kerberos, as informações contidas no PAC são usadas para gerar o token de acesso do usuário. O cliente apresenta o token ao computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte do pacote de logon.  
  
 Se o token foi criado incorretamente ou danificado durante transmissão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode oferecer informações adicionais sobre o problema.  
  
 Quando o usuário é membro de muitos grupos ou tem muitas políticas, o token pode ficar maior do que o normal para listar todos esses itens. Se o token ficar maior que o valor de **MaxTokenSize** do computador servidor, a conexão do cliente falhará com um GNE (Erro Geral de Rede) e um erro 17832 poderá ocorrer. Este problema pode afetar apenas alguns usuários: usuários com muitos grupos ou políticas. Quando o problema for o valor de **MaxTokenSize** do computador servidor, o erro 17832 no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será acompanhado por um erro com o estado 9. Para obter mais detalhes sobre o Kerberos e **MaxTokenSize**, consulte [KB327825](https://support.microsoft.com/kb/327825).  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver esse problema, aumente o valor de **MaxTokenSize** do computador servidor para um tamanho grande o suficiente para conter o maior token de qualquer usuário da organização. Para pesquisar o tamanho de token correto para sua organização, considere o uso do aplicativo **Tokensz**.   
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 **Para alterar o MaxTokenSize no computador do servidor**  
  
1.  No menu **Iniciar** , clique em **Executar**.  
  
2.  Digite `regedit` e clique em **OK**. (Se a caixa de diálogo **Controle de Conta de Usuário** for exibida, clique em **Continuar**.)  
  
3.  Navegue para **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters**.  
  
4.  Se o parâmetro **MaxTokenSize** não estiver presente, clique com o botão direito do mouse em **Parâmetros**, aponte para **Novo** e clique no Valor **DWORD (32 bits)** . Nomeie a entrada de Registro **MaxTokenSize**.  
  
5.  Clique com o botão direito do mouse em **MaxTokenSize** e clique em **Modificar**.  
  
6.  Na caixa **Dados de valor**, digite o valor desejado de **MaxTokenSize**.  
  
    > [!NOTE]  
    >  O valor hexadecimal ffff (valor decimal 65535) corresponde ao tamanho de token máximo recomendado. O fornecimento desse valor provavelmente resolverá o problema, mas talvez tenha efeitos negativos no computador em relação ao desempenho. Recomendamos que você estabeleça o valor mínimo de **MaxTokenSize** que permita o maior token de qualquer usuário da organização e insira esse valor.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Feche o **Editor do Registro**.  
  
9. Reinicie o computador.  
  
  
