LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')
NAMESPACE = os.getenv("NAMESPACE", default='default')

k8s_custom_deploy(
    'yo',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --update-strategy replace --debug --live-update" +
               " --local-path " + LOCAL_PATH +
               " --namespace " + NAMESPACE +
               " --yes --output yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace " + NAMESPACE + " --yes",
    container_selector='workload',

    # Live Update VScode:
    deps=['build.gradle.kts', './bin/main'],
    live_update=[
        sync('./bin/main', '/workspace/BOOT-INF/classes')
    ]
)

k8s_resource('yo', port_forwards=["8080:8080"],
            extra_pod_selectors=[{'carto.run/workload-name': 'yo', 'app.kubernetes.io/component': 'run'}])
