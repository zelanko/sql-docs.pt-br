---
title: Adicionar um instantâneo ao histórico de relatórios (Gerenciador de Relatórios) | Microsoft Docs
ms.prod: reporting-services-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: ba994e3fe63bfabeb9949f6dc96dc4b4536f0f0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568540"
---
# <a name="add-a-snapshot-to-report-history-report-manager"></a>Adicionar um instantâneo ao histórico de relatório (Gerenciador de Relatórios)

O histórico de relatórios é uma coleção de instantâneos de relatórios que você cria. Um instantâneo de relatório é um relatório que contém informações sobre layout e resultados de consulta que foram recuperados em um momento determinado. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  
  
## <a name="to-manually-add-snapshots-to-report-history"></a>Para adicionar manualmente instantâneos ao histórico de relatórios
  
::: moniker range="<=sql-server-2016||=sqlallproducts-allversions"

1. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.
  
2. No menu suspenso, clique em **Exibir Histórico de Relatório**.  
  
3. Clique em **Novo Instantâneo**. Um novo instantâneo é criado na coluna **Quando Executado** .  
  
    > [!NOTE]
    > Para fazer isso, o histórico de relatório deve ser configurado pelo administrador como **Permitir que o histórico seja criado manualmente**. Para obter mais informações, consulte [Limitar o histórico de relatório &#40;Gerenciador de Relatórios&#41;](../reports/limit-report-history-report-manager.md).

4. Clique em **Aplicar**.

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

1. No Gerenciador de Relatórios, navegue até a página **Conteúdo**, focalize o item cujo histórico você quer exibir e clique nas reticências (...).

2. No menu suspenso, clique em **Exibir Histórico de Relatório**.  

3. Clique em **novo instantâneo de histórico**. Um novo instantâneo é criado e listado.

    > [!NOTE]  
    > Para fazer isso, o histórico de relatório deve ser configurado pelo administrador como **Permitir que o histórico seja criado manualmente**. Para obter mais informações, consulte [Limitar o histórico de relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/limit-report-history-report-manager.md).

4. Clique em **Aplicar**.

::: moniker-end
  
### <a name="to-automatically-add-all-snapshots-to-report-history"></a>Para adicionar automaticamente todos os instantâneos ao histórico de relatórios  
  
1. Para um relatório que já foi configurado para ser executado como um instantâneo de execução de relatório, é possível definir propriedades adicionais para salvar uma cópia do instantâneo no histórico de relatórios sempre que o instantâneo for atualizado.  
  
2. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.  
  
3. No menu suspenso, clique em **Gerenciar**.  
  
4. Clique em **Opções de Instantâneo**.  
  
5. Marque a caixa de seleção **Armazenar todos os instantâneos de execução de relatórios no histórico**.  
  
6. Clique em **Aplicar**.  
  
### <a name="to-automatically-add-snapshots-to-report-history-based-on-a-schedule"></a>Para adicionar automaticamente instantâneos ao histórico de relatórios com base em um agendamento  
  
1. No Gerenciador de Relatórios, navegue até a página **Conteúdo** , focalize o item cujo histórico você quer exibir e clique na seta suspensa.  
  
2. No menu suspenso, clique em **Gerenciar**.  
  
3. Clique em **Opções de Instantâneo**.  
  
4. Marque a caixa de seleção para **Usar o agendamento a seguir para adicionar instantâneos ao histórico de relatório**. Execute um destes procedimentos:  
  
    - Selecione **Agendamento específico do relatório**. Preencha os detalhes do agendamento, selecione as datas de início e término e clique em **OK**.  

    - Selecione **Agendamento compartilhado**. Na lista, selecione a agenda desejada.  

5. Clique em **Aplicar**.  
  
## <a name="see-also"></a>Confira também

- [Configurar propriedades de execução de um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)
- [Abrir e fechar um relatório &#40;Gerenciador de relatórios&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)- [limitar o histórico de relatório &#40;Gerenciador de relatórios&#41;](../../reporting-services/reports/limit-report-history-report-manager.md)
- [Agendas](../../reporting-services/subscriptions/schedules.md)   
- [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)
