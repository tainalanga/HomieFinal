# HomieFinal

 $tpl->show();
    })->add($dashboardMW);

    $app->get('/dashboard/imovel/alugar[/{id:.*}]', function ($request, $response, $args) use ($tpl, $templates) {
        $tpl->addFile("CONTEUDO_DASHBOARD", $templates['dashboard/imovel/novoImovel']);
        $error = 0;
        if($error == 0){
            $imovel = new Imoveis($args['id']);
            if(!empty($args['id'])){
                if($imovel->imovel['vagas']>0){
                    $vagas = $imovel->imovel['vagas'] - 1 ;
                    $imovel->alugar($vagas, $args['id']);
                    return $response->withRedirect($this->router->pathFor('dashboard')); 
                }
                else{

                    $tpl->AVISO = '<script>window.alert("SEM VAGAS");</script>';
                }
            }
        }

        $tpl->show();
    })->add($dashboardMW);

    $app->get('/dashboard/imovel/desalugar[/{id:.*}]', function ($request, $response, $args) use ($tpl, $templates) {
        $tpl->addFile("CONTEUDO_DASHBOARD", $templates['dashboard/imovel/novoImovel']);
        $error = 0;
        if($error == 0){
            $imovel = new Imoveis($args['id']);
            if(!empty($args['id'])){
                if($imovel->imovel['vagas'] < $imovel->imovel['limite_pessoas']){
                    $vagas = $imovel->imovel['vagas'] + 1 ;
                    $imovel->alugar($vagas, $args['id']);
                    return $response->withRedirect($this->router->pathFor('dashboard')); 
                }
                else{

                    $tpl->AVISO = '<script>window.alert("maximo de vagas");</script>';
                }
            }
        }

        $tpl->show();
    })->add($dashboardMW);
