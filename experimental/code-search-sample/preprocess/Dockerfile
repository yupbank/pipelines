FROM python:2

RUN git clone --branch=master --depth=1 https://github.com/kubeflow/examples && \
    python2 -m pip install --user -r examples/code_search/src/requirements.txt

# Downloading gcloud package
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz

# Installing the package
RUN mkdir -p /usr/local/gcloud \
  && tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz \
  && /usr/local/gcloud/google-cloud-sdk/install.sh

# Adding the package path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

WORKDIR examples/code_search/src

ENTRYPOINT ["/bin/bash", "-c", "gcloud auth activate-service-account --key-file=${GOOGLE_APPLICATION_CREDENTIALS} && python2 -m code_search.dataflow.cli.preprocess_github_dataset"]
#
#
#
#
## parameterize
#export PROJECT='kubeflow-dev'
#export TARGET_DATASET='code_search'
#export WORKING_DIR='gs://kubeflow-examples/t2t-code-search/notebook-demo'
#export RESULT_DIR = 'gs://yang-kubeflow-examples/dataflow'
#export WORKER_MACHINE_TYPE='n1-highcpu-32'
#export NUM_WORKERS=16
#
#
#
#
#
#
#cd examples/code_search/src
#
#JOB_NAME="preprocess-github-dataset-$(date +'%Y%m%d-%H%M%S')"
#
#
#
#python2 -m code_search.dataflow.cli.preprocess_github_dataset \
#        --runner DataflowRunner \
#        --project "${PROJECT}" \
#        --target_dataset "${TARGET_DATASET}" \
#        --data_dir "${WORKING_DIR}/data" \
#        --job_name "${JOB_NAME}" \
#        --temp_location "${RESULT_DIR}/temp" \
#        --staging_location "${RESULT_DIR}/staging" \
#        --worker_machine_type "${WORKER_MACHINE_TYPE}" \
#        --num_workers "${NUM_WORKERS}"
#
