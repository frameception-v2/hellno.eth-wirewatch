Convert raw user description and API context into an implementation-ready specification.
Make sure we provide a functional web app that meets the user requirements.
Be concise and clear in your documentation.
There is no database available for this project.
We have an existing Farcaster miniapp (Frame v2) template to work with.
We need to customize the template in form and function to meet the user requirements.

## API Context
- allOf:
                                    - *id004
                                    - type: object
                                      required:
                                      - type
                                      - url
                                      - width
                                      - height
                                      properties:
                                        type:
                                          type: string
                                          enum:
                                          - photo
                                        url:
                                          type:
                                          - string
                                          - 'null'
                                          description: The source URL of the image.
                                            Consumers should be able to insert this
                                            URL into an <img> element. Only HTTP and
                                            HTTPS URLs are valid.
                                        width:
                                          type:
                                          - number
                                          - 'null'
                                          description: The width in pixels of the
                                            image specified in the url parameter.
                                        height:
                                          type:
                                          - number
                                          - 'null'
                                          description: The height in pixels of the
                                            image specified in the url parameter.
                                  - allOf:
                                    - *id004
                                    - type: object
                                      required:
                                      - type
                                      properties:
                                        type:
                                          type: string
                                          enum:
                                          - link
                                  discriminator:
                                    propertyName: type
                                    mapping:
                                      rich: '#/components/schemas/OembedRichData'
                                      video: '#/components/schemas/OembedVideoData'
                                      photo: '#/components/schemas/OembedPhotoData'
                                      link: '#/components/schemas/OembedLinkData'
                          frame: &id011
                            discriminator:
                              propertyName: version
                            oneOf:
                            - description: Frame v1 object
                              allOf:
                              - &id005
                                description: Frame base object used across all versions
                                type: object
                                required:
                                - version
                                - image
                                - frames_url
                                properties:
                                  version:
                                    type: string
                                    description: Version of the frame, 'next' for
                                      v2, 'vNext' for v1
                                  image:
                                    type: string
                                    description: URL of the image
                                  frames_url:
                                    type: string
                                    description: Launch URL of the frame
                              - type: object
                                properties:
                                  buttons:
                                    type: array
                                    items:
                                      type: object
                                      required:
                                      - index
                                      - action_type
                                      properties:
                                        title:
                                          type: string
                                          description: Title of the button
                                        index:
                                          type: integer
                                          description: Index of the button
                                        action_type:
                                          type: string
                                          description: The action type of a frame
                                            button. Action types "mint" & "link" are
                                            to be handled on the client side only
                                            and so they will produce a no/op for POST
                                            /farcaster/frame/action.
                                          enum:
                                          - post
                                          - post_redirect
                                          - tx
                                          - link
                                          - mint
                                        target:
                                          type: string
                                          description: Target of the button
                                        post_url:
                                          type: string
                                          description: Used specifically for the tx
                                            action type to post a successful transaction
                                            hash
                                  post_url:
                                    type: string
                                    description: Post URL to take an action on this
                                      frame
                                  title:
                                    type: string
                                  image_aspect_ratio:
                                    type: string
                                  input:
                                    type: object
                                    properties:
                                      text:
                                        type: string
                                        description: Input text for the frame
                                  state:
                                    type: object
                                    properties:
                                      serialized:
                                        type: string
                                        description: State for the frame in a serialized
                                          format
                            - description: Frame v2 object
                              allOf:
                              - *id005
                              - type: object
                                required:
                                - title
                                - name
                                - icon
                                properties:
                                  manifest:
                                    type: object
                                    properties:
                                      account_association:
                                        type: object
                                        properties:
                                          header:
                                            type: string
                                          payload:
                                            type: string
                                          signature:
                                            type: string
                                        required:
                                        - header
                                        - payload
                                        - signature
                                      frame:
                                        type: object
                                        properties:
                                          version:
                                            type: string
                                            enum:
                                            - 0.0.0
                                            - 0.0.

- allOf:
                                - *id003
                                - type: object
                                  required:
                                  - type
                                  - url
                                  - width
                                  - height
                                  properties:
                                    type:
                                      type: string
                                      enum:
                                      - photo
                                    url:
                                      type:
                                      - string
                                      - 'null'
                                      description: The source URL of the image. Consumers
                                        should be able to insert this URL into an
                                        <img> element. Only HTTP and HTTPS URLs are
                                        valid.
                                    width:
                                      type:
                                      - number
                                      - 'null'
                                      description: The width in pixels of the image
                                        specified in the url parameter.
                                    height:
                                      type:
                                      - number
                                      - 'null'
                                      description: The height in pixels of the image
                                        specified in the url parameter.
                              - allOf:
                                - *id003
                                - type: object
                                  required:
                                  - type
                                  properties:
                                    type:
                                      type: string
                                      enum:
                                      - link
                              discriminator:
                                propertyName: type
                                mapping:
                                  rich: '#/components/schemas/OembedRichData'
                                  video: '#/components/schemas/OembedVideoData'
                                  photo: '#/components/schemas/OembedPhotoData'
                                  link: '#/components/schemas/OembedLinkData'
                      frame: &id010
                        discriminator:
                          propertyName: version
                        oneOf:
                        - description: Frame v1 object
                          allOf:
                          - &id004
                            description: Frame base object used across all versions
                            type: object
                            required:
                            - version
                            - image
                            - frames_url
                            properties:
                              version:
                                type: string
                                description: Version of the frame, 'next' for v2,
                                  'vNext' for v1
                              image:
                                type: string
                                description: URL of the image
                              frames_url:
                                type: string
                                description: Launch URL of the frame
                          - type: object
                            properties:
                              buttons:
                                type: array
                                items:
                                  type: object
                                  required:
                                  - index
                                  - action_type
                                  properties:
                                    title:
                                      type: string
                                      description: Title of the button
                                    index:
                                      type: integer
                                      description: Index of the button
                                    action_type:
                                      type: string
                                      description: The action type of a frame button.
                                        Action types "mint" & "link" are to be handled
                                        on the client side only and so they will produce
                                        a no/op for POST /farcaster/frame/action.
                                      enum:
                                      - post
                                      - post_redirect
                                      - tx
                                      - link
                                      - mint
                                    target:
                                      type: string
                                      description: Target of the button
                                    post_url:
                                      type: string
                                      description: Used specifically for the tx action
                                        type to post a successful transaction hash
                              post_url:
                                type: string
                                description: Post URL to take an action on this frame
                              title:
                                type: string
                              image_aspect_ratio:
                                type: string
                              input:
                                type: object
                                properties:
                                  text:
                                    type: string
                                    description: Input text for the frame
                              state:
                                type: object
                                properties:
                                  serialized:
                                    type: string
                                    description: State for the frame in a serialized
                                      format
                        - description: Frame v2 object
                          allOf:
                          - *id004
                          - type: object
                            required:
                            - title
                            - name
                            - icon
                            properties:
                              manifest:
                                type: object
                                properties:
                                  account_association:
                                    type: object
                                    properties:
                                      header:
                                        type: string
                                      payload:
                                        type: string
                                      signature:
                                        type: string
                                    required:
                                    - header
                                    - payload
                                    - signature
                                  frame:
                                    type: object
                                    properties:
                                      version:
                                        type: string
                                        enum:
                                        - 0.0.0
                                        - 0.0.

## User Requirements
build a frame that forwards the visitor to the website  https://corporate.watch

## Output Format
1. Markdown document with these sections:
   - Functional User Requirements
   - Architecture Diagram
   - Data Flow Specification
   - Error Handling Strategies
2. Technical terms clearly defined
