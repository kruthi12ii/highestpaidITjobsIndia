import os
import boto3


s3_client = boto3.client(
    's3',
    aws_access_key_id='',
    aws_secret_access_key=''
)


def upload_files_s3():
    
    #use boto3 library

    #https://boto3.amazonaws.com/v1/documentation/api/latest/guide/s3-uploading-files.html
    # """Upload a file to an S3 bucket

    # :param file_name: File to upload
    # :param bucket: Bucket to upload to
    # :param object_name: S3 object name. If not specified then file_name is used
    # :return: True if file was uploaded, else False
    # """

    # # If S3 object_name was not specified, use file_name
    # if object_name is None:
    #     object_name = os.path.basename(file_name)

    # # Upload the file
    # s3_client = boto3.client('s3')
    # try:
    #     response = s3_client.upload_file(file_name, bucket, object_name)
    # except ClientError as e:
    #     logging.error(e)
    #     return False
    # return True
    local_dir_path = r"D:\highestpaidsalary"  
    bucket_name = 'highestpaidjobss'

    

    # Specify the filenames of the files you want to upload
    files_to_upload = [
        'highestpaidjobss.csv',
    ]

    try:
        for filename in files_to_upload:
            local_file_path = os.path.join(local_dir_path, filename)
            object_name = os.path.basename(local_file_path)

            # Upload the file to S3 bucket
            s3_client.upload_file(local_file_path, bucket_name, object_name)

            print(f"File '{filename}' uploaded successfully to S3 bucket '{bucket_name}' as '{object_name}'")

        return True

    except Exception as e:
        print(f"An exception occurred while uploading files to S3: {e}")
        return False

# Example usage:
if __name__ == "__main__":
    upload_files_s3()


    pass
